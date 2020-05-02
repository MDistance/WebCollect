### 插槽
    插槽是一种父子组件传递html模板的技术
    2.6之前的版本
        普通插槽
            父(模板):
                <v-child>
                    <template>
                        来自于父组件的html的片段
                    </template>
                </v-child>
            子(模板):
                <div>
                    <slot>
                        默认的html片段
                    </slot>
                </div>
            效果:
                  在子模板覆盖掉父模板中的v-child时;template中的内容会覆盖掉整个slot;
                  如果父模板没有准备html片段;那么slot中的默认的html片段会被启用
        具名插槽
            父(模板):
                <v-child>
                    <template slot="a">
                        来自于父组件的html的片段-1
                    </template>
                    <template slot="b">
                        来自于父组件的html的片段-2
                    </template>
                </v-child>
            子(模板):
                <div>
                    <slot name="a"></slot>
                    <slot name="b"></slot>
                </div>
            效果:
                  在子模板覆盖掉父模板中的v-child时;template中的内容会按名字覆盖掉对应的slot
        作用域插槽
            父(模板):
                <v-child>
                    <template slot="a" slot-scope="obj">
                        来自于父组件的html的片段-1
                    </template>
                    <template slot="b" slot-scope="{damu,xfz}">
                        来自于父组件的html的片段-2
                    </template>
                </v-child>
            子(模板):
                <div>
                    <slot name="a" damu="damu" xfz="xfz"></slot>
                    <slot name="b" damu="damu" xfz="xfz"></slot>
                </div>
            效果:
                  在子模板覆盖掉父模板中的v-child时;template中的内容会按名字覆盖掉对应的slot
                  而且slot上自定义的标签属性会被收集到 template指定的对象中(obj)
    2.6之后的版本
        普通插槽
            与2.6之前的版本保持了一致
        具名插槽
            template上的slot属性 被替换成了一个指令v-slot
                <template slot="a">
                   来自于父组件的html的片段-1
                </template>
                <template v-slot:a>
                   来自于父组件的html的片段-1
                </template>
                <template #a>
                   来自于父组件的html的片段-1
                </template>
        作用域插槽
            template上的slot-scope属性 被替换成了一个指令v-slot
                <template slot="a" slot-scope="obj">
                    来自于父组件的html的片段-1
                </template>
                <template v-slot:a="obj">
                   来自于父组件的html的片段-1
                </template>
                 <template #a="obj">
                   来自于父组件的html的片段-1
                </template>