# basic-juggler

# basic-juggler是一个动画管理类，可以添加与移除动画

### 依赖basic-help，basic-event

### 快速开始：

    npm install basic-juggler

### 如何使用：

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <script src="../basic-help/dist/basic-help.js" type="text/javascript"></script>
        <script src="../basic-event/dist/basic-event.js" type="text/javascript"></script>
        <script src="../basic-juggler/dist/basic-juggler.js" type="text/javascript"></script>
        <script type="text/javascript">
            function View() {
                this.isAdd = false;
                this.advanceTime = function (time) {
                    if (!this.isAdd) {
                        //回调是移除其他对象，如果移除的对象在这次调用后，则不再调用
                        movie1.dispatchEventWith(basic.jugglerEventType.REMOVE_FROM_JUGGLER);
                        //回调时添加的新对象，不作处理，下一帧再处理
                        var view1 = new View1();
                        basic.jugglerManager.juggler.add(view1);
                        this.isAdd = true;
                    }
                }
            }
            function View1() {
                this.advanceTime = function (time) {
                }
            }
            function Movie() {
                this.isRemove = false;
                basic.EventDispatcher.apply(this);
                this.advanceTime = function (time) {
                    if (!this.isRemove) {
                        basic.jugglerManager.juggler.remove(movie2);
                        this.isRemove = true;
                    }
                }
            }
            function Movie1() {
                basic.EventDispatcher.apply(this);
                this.advanceTime = function (time) {

                }
            }
            var view = new View();
            var movie = new Movie();
            var movie1 = new Movie1();
            var movie2 = new Movie1();
            window.onload = function () {
                basic.jugglerManager.juggler.add(view);
                basic.jugglerManager.juggler.add(movie1);
                basic.jugglerManager.juggler.add(movie2);
                basic.jugglerManager.juggler.add(movie);
            }
        </script>
    </head>
    <body>

    </body>
    </html>


### 注意：

    1、回调中新加入的动画不能在这一次被调度，因为没有经历时间过程这是合理的
    2、回调中移除的分两种可能，已经在本次调度的无影响，没有在本次调度的取消本次调度



	