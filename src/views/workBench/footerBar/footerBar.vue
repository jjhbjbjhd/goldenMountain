<template>
    <div class="mi-footerBar__main">
        <div>[x]文件状态(已保存)</div>
        <div>平均:1,计数:3,求和:3</div>
        <div>行4,列18(已选择3行,4列)</div>
        <div>[x]You,4个月前(历史)</div>
        <div>[x]Lsw,一分钟前(评论)</div>
        <div>[x]在线/断开链接</div>
        <div>[x]通知(+4)</div>
    </div>
</template>

<style>
.mi-footerBar__main{
    width:100%;
    height: 35px;
    bottom: 0px;
    background-color:#1A7B42;
    position: fixed;
    display: flex;

    & div{
        height:100%;
        width: 250px;
        color: white;
        padding: 0%;
        font-size: 14px;
        font-weight: 500;
        text-align: center;
        line-height: 35px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    & div:hover {
        cursor: pointer;
        background-color: rgba(255,255, 255, 0.1);
    }
}

</style>