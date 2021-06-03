```html
<div class="title m-b-20">
  <div class="bg-grp">
    <div class="bg-left">
      <p></p >
    </div>
    <div class="bg-right">
      <p></p >
      <p></p >
      <p></p >
    </div>
  </div>
  <div class="font-grp">
    <img src="@/assets/images/province/left.png" alt="" />
    <p>申报主体区域分布</p >
  </div>
</div>
```



```less
.title {
  margin-bottom: 20px;
  position: relative;
  .bg-grp {
    display: flex;
    .bg-left {
      width: calc(100% - 42px);
      background: #568eff;
      height: 25px;
      position: relative;
      p {
        margin: 0;
        width: 0;
        height: 0;
        border-bottom: 25px solid #fff;
        border-left: 12px solid transparent;
        position: absolute;
        right: 0;
      }
    }
    .bg-right {
      display: flex;
      p {
        margin: 0;
        margin-left: 5px;
        width: 6px;
        height: 25px;
        transform: skewX(155deg);
      }
      p:first-child {
        margin-left: 0;
        background: rgba(86, 142, 255, 0.7);
      }
      p:nth-child(2) {
        background: rgba(86, 142, 255, 0.4);
      }
      p:nth-child(3) {
        background: rgba(86, 142, 255, 0.2);
      }
    }
  }
  .font-grp {
    position: absolute;
    top: 0;
    left: 13px;
    display: flex;
    align-items: center;
    p {
      margin: 0;
      margin-left: 10px;
      color: #fff;
      font-weight: 600;
      font-size: 16px;
    }
  }
}
```

