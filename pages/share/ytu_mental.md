# YTU 心理评测自动化脚本

打开答题页面后，按 F12 打开开发者工具，切换到 Console（控制台） 标签，粘贴以下代码并回车。随后当前页面会立即自动切题、答题，并显示一个巨大的停止按钮。再答完题后，点击停止按钮即可停止自动化脚本。

```javascript
let radio = 'div.question_info > ul > li:nth-child(1)'
let button = '#main-box > div > div > div > div:nth-child(2) > div > div > div.question_btn.question_btn2 > div.next_btn > div:nth-child(1)'

function clickOnce() {
    let r = document.querySelector(radio);
    if (r == null) {
        return false;
    }
    let b = document.querySelector(button);
    r.click();
    b.click();
    return true;
}

const timer = setInterval(function() {
    let flag = clickOnce();
    if (!flag) {
        console.log('did not find the button, now stopped.')
        clearInterval(timer);
    }
}, 200);

console.log('use clearInterval(timer) to stop this script');

function addStopButton() {
    let div = document.createElement("div");
    div.style.cssText = `
        position: fixed;
        display: flex;
        justify-content: center;
        align-items: center;
        right: 20px;
        top: 20px;
        width: 200px;
        height: 200px;
        z-index: 2000;
        border: 0px;
        background-image: linear-gradient(315deg, #B2B1B9, #FFFFFF, #B2B1B9);
        box-shadow: 6px 6px 18px rgba(0,0,0,0.5);
        border-radius: 8px;
    `;
    let button = document.createElement("button");
    button.style.cssText = `
        background: rgb(254,0,0);
        background: linear-gradient(305deg, rgba(254,0,0,1) 0%, rgba(249,105,2,1) 100%);
        font-weight: bold;
        font-size: 36px;
        width: 150px;
        height: 150px;
        border-radius: 50%;
        color: white;
        border: 0px;
        box-shadow: 6px 6px 18px rgba(0,0,0,0.5);
        cursor: pointer;
    `;
    button.innerHTML = "停止";
    button.addEventListener("click", function() {
        if (typeof timer !== 'undefined') clearInterval(timer);
        button.innerHTML = "OK!";
        setTimeout(function(){
            document.body.removeChild(div)
        }, 1000);
    });
    div.appendChild(button);
    document.body.appendChild(div);
}

addStopButton();
```