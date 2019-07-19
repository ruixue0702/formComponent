<template>
    <div>
        <ul>
            <item class="item" :model="treeData"></item>
        </ul>
    </div>
</template>

<script>
    import Item from "./Item";
    export default {
        data(){
            return {
                treeData: {
                    title: "一级树节点",
                    children: [
                    {
                        title: "二级树节点1"
                    },
                    {
                        title: "二级树节点2",
                        children: [
                        {
                            title: "三级树节点1"
                        },
                        {
                            title: "三级树节点2"
                        }
                        ]
                    },
                    {
                        title: "二级树节点3",
                        children: [
                        {
                            title: "三级树节点3",
                            expand: true,
                            children: [
                            {
                                title: "四级树节点1"
                            },
                            {
                                title: "四级树节点2"
                            },
                            {
                                title: "四级树节点3"
                            }
                            ]
                        },
                        {
                            title: "三级树节点4",
                            children: [
                            {
                                title: "四级树节点4"
                            },
                            {
                                title: "四级树节点5"
                            }
                            ]
                        },
                        {
                            title: "三级树节点5"
                        }
                        ]
                    }
                    ]
                }
            }
        },
        components: { Item }
    }
</script>

<style lang="scss" scoped>

</style>