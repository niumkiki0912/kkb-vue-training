###  

##### 问题

+ v-if和v-for哪个优先级更高? 如果两个同时出现,应该怎样优化得到更好的性能

##### 回答

+ 原则上不要把v-if和v-for放到同一个元素上。但是如果两者要是放到同一个元素上时，v-for比v-if具有更高的优先级，渲染模板时，相当于对每次遍历的结果进行了一次条件判断

+ 当两者同时出现时

  + 避免渲染本应该被隐藏的列表，将v-if移动至父节点上, 例如

    ```vue
    <ul v-if="lists.length">
      <li
          :key="list.id"
          v-for="list in lists">
        	{{list.name}}
      </li>
    </ul>
    ```

  + 如果是为了过滤列表中的项目, 在这种情况下可以使用计算属性,让其返回过滤后的列表

    ```vue
    // 原:
    <ul>
      <li
          v-for="list in lists"
          v-if="list.isActive"
          :key="list.id">
        	{{list.name}}
      </li>
    </ul>

    // 改为:
    <ul>
      <li
          v-for="list in activeLists"
          :key="list.id">
        	{{list.name}}
      </li>
    </ul>

    // computed
    export default {
    	computed: {
            activeLists () {
              return this.lists.filter( list => list.isActive)
            }
        }
    }


    ```

    ​