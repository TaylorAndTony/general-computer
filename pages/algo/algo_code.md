# 手敲代码算法实录

## 排序类

### 查找数组中第 k 大的元素

```c
#include <stdio.h>

// 找序列中第 k 大的数
int kth_element(int a[], int low, int high, int k)
{
    // 先正常快速排序划分序列
    int pivot = a[low];
    int _low = low;
    int _high = high;
    while (low < high)
    {
        // 右指针左移，找第一个小于 pivot 的
        while (low < high && a[high] >= pivot)
        {
            --high;
        }
        a[low] = a[high];
        // 左指针右移，找第一个大于 pivot 的
        while (low < high && a[low] <= pivot)
        {
            ++low;
        }
        a[high] = a[low];
    }
    // pivot 进序列（因为前面直接覆盖了 pivot 的值
    a[low] = pivot;
    // 下面是精髓
    // 当 low 等于 k 时，说明划分的位置正好就是要的
    if (low == k)
    {
        return a[low];
    }
    // 若小于给定值，说明给定值一定在右边的部分。递归处理右侧序列即可
    // 画个图：
    // [ ... ... ... ] low [ ... ... ...]
    // 1             2     3            4
    //
    // 1: _low
    // 2: low - 1
    // 3: low + 1
    // 4: _high
    else if (low < k)
    {
        return kth_element(a, low + 1, _high, k);
    }
    // 若大于，则一定在左边的部分
    else
    {
        return kth_element(a, _low, low - 1, k);
    }
}

int main()
{
    int a[] = {4, 5, 6, 1, 2, 3, 7};
    int k = 3;
    int result = kth_element(a, 0, sizeof a / sizeof a[0], k);
    printf("%d-th big element is %d", k, result);
    return 0;
}
```

### 三色国旗

给定一个包含红白蓝颜色的乱序序列，按线性复杂度排序，让其符合“红白蓝”顺序。算法必须满足 O(n) 的时间复杂度。

如：{0,1,2,2,1,0} -> {0,0,1,1,2,2}

```c
#include <stdio.h>

enum
{
    RED,
    WHITE,
    BLUE
} colors;

void swap(int list[], int index1, int index2)
{
    int t = list[index1];
    list[index1] = list[index2];
    list[index2] = t;
}

void print_array(int a[], int n)
{
    for (int i = 0; i < n; i++)
    {
        printf("%d, ", a[i]);
    }
}

void flags(int color[], int n)
{
    int first = 0, working = 0, last = n - 1;
    while (working < last)
    {
        switch (color[working])
        {
        case RED:
            // RED 要排在第一位，永远与低指针交换
            swap(color, first, working);
            first++;
            working++;
            break;

        case BLUE:
            // BLUE 永远与高指针交换
            swap(color, working, last);
            // 高指针降低一位
            last--;
            // 再次处理此情况，不要后移工作指针
            // 因为交换后，working 仍可能是 BLUE
            break;

        case WHITE:
            // 遇到在中间的，跳过即可
            working++;
            break;
        default:
            break;
        }
    }
}

int main()
{
    int flag[] = {0,1,2,2,1,0};
    flags(flag, 6);
    print_array(flag, 6);
    return 0;
}
```