# Malloc

## 相关问题

### malloc（0）会发生什么
* C标准中并没有定义这样的一个行为具体行为，而是由实现者自行定义
* glibc（最新版本2.38）里面对于malloc(0)的定义是返回一个小内存块
  * 32位下是16字节
  * 64位下是24字节或者32字节（在本机跑了是24字节）

### new和malloc区别
* https://www.cnblogs.com/qg-whz/p/5140930.html

### 谁来保存free的大小
* 简单来说
  * 空间的大小记录在参数指针指向地址的前面，free的时候通过这个记录即可知道要释放的内存有多大。
https://www.zhihu.com/question/302440083

```
#include <bits/stdc++.h>

using namespace std;

struct mem {
  long addr;
  long len;
  mem(int a, long l): addr(a), len(l) {}
  bool operator< (const mem &other) const {
      if(addr < other.addr) {
          return true;
      }
      return false;
  }
};

class MemPool {
private:
    unordered_map<long, long> allocation_map; // 已经分配出去的地址空间大小，addr->size
    vector<mem> free_list; // 还存在的地址空间 addr->size
public:
    MemPool(long a, long l) {
        free_list.push_back(mem(a, l));
        cout << "init success: addr: " << a << ", len:" << l << endl;
    }

    void* malloc(long size) {
        for(int i = 0; i < free_list.size(); i++) {
            mem m = free_list[i];
            if(m.len < size) {
                continue;
            }
            free_list.erase(free_list.begin()+i);
            if(m.len > size) {
                free_list.push_back(mem(m.addr+size, m.len - size));
            }
            allocation_map[m.addr] = size;
            cout << "allocate " << size << " mem success, from " << m.addr << endl;
            return reinterpret_cast<void*>(m.addr);
        }
        cout << "allocate " << size << " mem failed" << endl;
        return reinterpret_cast<void*>(-1);
    }

    void free(void* ptr) {
        if ((long)ptr != -1l) {
            long addr = (long)ptr;
            long len = allocation_map[addr];
            cout << "free mem from " << addr << ", size: " << len << endl;
            allocation_map.erase(addr);
            free_list.push_back(mem(addr, len));
        }
        compact();
    }
    
    void print_cur() {
        cout << "cur free list: " << endl;
        for(mem m: free_list) {
            cout << "    " << m.addr << "->" << m.addr + m.len << endl;
        }
    }
    
    void compact() {
        sort(free_list.begin(), free_list.end());
        vector<mem> new_free_list;
        if(free_list.empty()) {
            return;
        }
        new_free_list.push_back(free_list[0]);
        for(int i = 1; i < free_list.size(); i++) {
            if(new_free_list.back().addr + new_free_list.back().len == free_list[i].addr) {
                new_free_list.back().len += free_list[i].len;
            } else {
                new_free_list.push_back(free_list[i]);
            }
        }
        free_list.swap(new_free_list);
    }

};

int main() {
    MemPool mempool(0, 28);
    mempool.print_cur();
    void* p1 = mempool.malloc(10);
    mempool.print_cur();
    void* p2 = mempool.malloc(10);
    mempool.print_cur();
    void* p3 = mempool.malloc(10);
    mempool.free(p2);
    mempool.print_cur();
    mempool.free(p1);
    mempool.print_cur();
    void* p4 = mempool.malloc(20);
    mempool.print_cur();
    mempool.free(p4);
    mempool.print_cur();
}
           
```
