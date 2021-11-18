
## question structure

### link

```json
141. Linked List Cycle(simple)
    142. Linked List CycleII(medium)
        287. Find the Duplicate Number(medium)
            136. 只出现一次的数字(simple)[<=R3]
                268. Missing Number(simple)[<=R3]
                    389. Find the Difference(simple)[R3]
```


#### link explain

- `389. Find the Difference(simple)` TODO:other resolution

    ```go
    //math resolution
    func findTheDifference(s string, t string) byte {
        sum := 0
        for _, ch := range s {
            sum += int(ch)
        }

        for _, ch := range t {
            sum -= int(ch)
        }

        if sum < 0 {
            sum = 0 - sum
        }

        return byte(sum)
    }
    ```


- `268. Missing Number(simple)`

    ```go
    //normal resolution
    func missingNumber(nums []int) int {
        cache := make(map[int]int)
        len := len(nums)

        for i := 0; i < len ; i++ {
            cache[nums[i]]++
        }

        for i:= 0; i <= len; i++ {
            if _, ok := cache[i]; !ok {
                return i
            }
        }

        return 0
    }

    //binary resolution
    func missingNumber(nums []int) int {
        len := len(nums)
        n := 0

        for i := 0; i < len ; i++ {
            n ^= nums[i]
            n ^= i
        }

        n ^= len

        return n
    }

    //binary resolution II(*)
    //if equal, missing number's bit must be 0
    //if noteuqal, missing number's bit must be 1
    func missingNumber(nums []int) int {
        len := len(nums)
        r := 0

        for i := 0; i < 32; i++ {
            normal := 0
            current := 0
            for j := 0; j <= len ; j++ {
                normal += (j >> i) & 0x1
                if j < len {
                    current += (nums[j] >> i) & 0x1
                }
            }

            if normal != current {
                r |= (1 << i)
            }
        }

        return r
    }

    //math resolution:高斯求和公式
    func missingNumber(nums []int) int {
	n := len(nums)

    sum := n * (n+1) / 2

    currentSum := 0
    for _, elem := range nums {
        currentSum += elem
    }

    return sum - currentSum
    }

    ```

- `136. 只出现一次的数字(simple)`
    
    ```go
    //normal resolution
    func singleNumber(nums []int) int {
        cache := make(map[int]int)


        for i := 0; i < len(nums); i++ {
            cache[nums[i]] += 1
        }

        for i := 0; i < len(nums); i++ {
            if cache[nums[i]] == 1 {
                return nums[i]
            }
        }

        return 0
    }

    //binary resolution
    //knowladge:a^a = 0 a^b^a=a^a^b=b a^0=a
    func singleNumber(nums []int) int {
        r := 0


        for _, elem := range nums {
            r ^= elem
        }


        return r
        
    }
    ```

## temp



```bash

digraph Link {

    start[label="2. Add Two Numbers(medium)", shape="box"]
    Multiply_Strings[label="Multiply Strings(medium)", shape="box"]
    Add_Binary[label="Add Binary(simple)", shape="box"]
    Sum_of_Two_Integers[label="Sum of Two Integers(medium)", shape="box"]
    Add_Strings[label="Add Strings(simple)", shape="box"]
    Add_Two_Numbers_II[label="Add Two Numbers II(medium)", shape="box"]
    Add_to_Array_Form_of_Integer[label="Add to Array-Form of Integer(simple)", shape="box"]

    start -> Multiply_Strings
    start -> Add_Binary
    start -> Sum_of_Two_Integers
    start -> Add_Strings
    start -> Add_Two_Numbers_II
    start -> Add_to_Array_Form_of_Integer

    Linked_List_Cycle[label="141. Linked List Cycle(simple)", shape="box"]
    Linked_List_CycleII[label="142. Linked List CycleII(medium)", shape="box"]
    Find_the_Duplicate_Number[label="287. Find the Duplicate Number(medium)", shape="box"]


    Linked_List_Cycle -> Linked_List_CycleII -> Find_the_Duplicate_Number

}

digraph demo {
    label="示例"
    bgcolor="beige"

    node[color="grey"]

    father[label="爸爸", shape="box"]
    mother[label="妈妈", shape="box"]
    brother[label="哥哥", shape="circle"]
    sister[label="姐姐", shape="circle"]
    node[color="#FF6347"]
    strangers[label="路人"]

    edge[color="#FF6347"]

    father->mother[label="夫妻", dir="both"]
    father->brother[label="父子"]
    father->sister[label="父子"]
    father->我[label="父子"]

    mother->{brother,sister,我}[label="母子"]

    {rank=same; father, mother}
    {rank=same; brother,sister,我}
}


digraph G {
    subgraph cluster0 {
        node [style=filled,color=white];
        style=filled;
        color=lightgrey;
        a0 -> a1 -> a2 -> a3;
        label = "process #1";
    }
    subgraph cluster1 {
        node [style=filled];
        b0 -> b1 -> b2 -> b3;
        label = "process #2";
        color=blue
    }
    start -> a0;
    start -> b0;
    a1 -> b3;
    b2 -> a3;
    a3 -> a0;
    a3 -> end;
    b3 -> end;
    start [shape=Mdiamond];
    end [shape=Msquare];
}

digraph G {
    compound=true;
    subgraph cluster0 {
        a -> b;
        a -> c;
        b -> d;
        c -> d;
    }
    subgraph cluster1 {
        e -> g;
        e -> f;
    }
    b -> f [lhead=cluster1];
    d -> e;
    c -> g [ltail=cluster0, lhead=cluster1];
    c -> e [ltail=cluster0];
    d -> h;
    cluster0->cluster1;
}
```


