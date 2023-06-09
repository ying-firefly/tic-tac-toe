# Tic Tac Toe

#### 介绍
井字棋，TypeScript

#### 软件架构
软件架构说明
IT黑马，链接：https://www.bilibili.com/video/BV1UD4y1m7Gw/?p=148&spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=10ee23f98948bf67d6868bf47b62adec

#### 安装教程

1.  xxxx
2.  xxxx
3.  xxxx

#### 使用说明

1.  玩法：两个玩家，一个玩家使用（X），一个玩家使用（O），轮流在棋盘上下棋（点击单元格）。
2.  获胜条件：横、竖、斜（对角线）三个棋子相同。
3.  平局：棋盘满子，但是，不满足任何一种获胜条件。

#### 总体思路

1. 游戏模板（HTML、CSS）的说明
   (1) 下一步提示：给游戏面板（#bord）标签，添加 x 或 o 类名。
   (2) 下棋（点击单元格）：给单元格（.cell）标签，添加 x 或 o 类名。
   (3) 展示和隐藏获胜信息：设置获胜信息面板（#message）标签的样式属性 display。
2. 点击下棋
   (1)单元格点击
      效果：点击棋盘的任意单元格，单元格显示 X（默认）。
      ① 获取到所有的单元格列表。
      ② 给当前被点击的单元格添加类名 x。
      ③ 遍历单元格列表，给每一个单元格添加点击事件。
      优化（1）：防止单元格重复点击，在添加事件时，使用 once 属性，让单元格只能被点击一次。
      优化（2）：使用函数声明形式的事件处理程序（代码多了后，代码结构会更清晰）。
   (2) 切换玩家
      效果：玩家（X）和玩家（O）轮流交替下棋。
      ① 创建一个存储当前玩家的变量（currentPlayer），默认值为：x。
      ② 切换到另一个玩家：在添加类名（下棋完成一步）后，根据当前玩家，得到另外一个玩家。
      ③ 将添加给单元格时写死的类名 x ，替换为变量（currentPlayer）的值。
      ④ 处理下一步提示：移除游戏面板中的 x 和 o 类名，添加下一个玩家对应的类名。
   (3) 使用枚举修改当前玩家
      效果：使用枚举代替原来的字符串类名（x 和 o）。
      ① 创建字符串枚举（Player），提供 X 和 O 两个成员。
      ② 将成员 X 的值设置为：'x'（类名）；将成员 O 的值设置为：'o'（类名）。
      ③ 将变量（currentPlayer）的类型设置为 Player 枚举类型，默认值为 Player.X。
      ④ 将所有用到 x 和 o 的地方全部使用枚举成员代替。
3. 游戏判赢
   (1) 判赢的思路
      思路：判断棋盘中，横、竖、斜（对角线）是否存在三个相同的 x 或 o。
           只要有一个满足条件，就说明 x 或 o 获胜了。
           如果所有单元格都有内容，但没有获胜的情况，就说明是平局。
   (2) 封装判赢函数
      ① 声明函数（checkWin），指定参数（player），类型注解为：Player 枚举。
      ② 指定返回值：现在函数中写死返回 true 或 false。
      ③ 在给单元格添加类名后（下棋后），调用函数 checkWin，拿到函数返回值。
      ④ 判断函数返回值是否为 true，如果是，说明当前玩家获胜了。
   (3) 实现判赢函数
      思路：遍历判赢数组，分别判断每种情况对应的 3 个单元格元素，是否同时包含当前玩家的类名。
      ① 使用 some 方法遍历数组，并将 some 方法的返回值作为判赢函数的返回结果。
      ② 在 some 方法的回调函数中，获取到每种获胜情况对应的 3 个单元格元素。
      ③ 判断这 3 个单元格元素是否同时包含当前玩家的类名。
      ④ 如果包含（玩家获胜），就在回调函数中返回 true 停止循环；否则，返回 false，继续下一次循环。
   (4) 优化判赢函数
      ① 去掉判赢函数的中间变量（isWin、cell1、cell2、cell3）。
      ② 封装函数（hasClass）：判断 DOM 元素是否包含某个类名。
   (5) 判断平局
      思路：创建变量（steps），记录已下棋的次数，判断 steps 是否等于 9，如果等于说明平局。
      注意：先判赢，再判断平局！
      ① 创建变量（steps），默认值为 0。
      ② 在玩家下棋后，让 steps 加 1。
      ③ 在判赢的代码后面，判断 steps 是否等于 9。
      ④ 如果等于 9 说明是平局，游戏结束，就直接 return，不再执行后续代码。
   (6) 展示获胜信息
      效果：在获胜或平局时，展示相应信息。
      ① 获取到与获胜信息相关的两个 DOM 元素：1 #message 2 #winner。
      ② 显示获胜信息面板（通过 style 属性实现）。
      ③ 展示获胜信息：如果获胜，展示“x 赢了！”或“o 赢了！”；如果是平局，展示“平局”。
4. 重新游戏
   效果：点击重新开始按钮，重新开始下棋游戏。
   说明：重新开始游戏，实际上就是要重置游戏中的所有数据，恢复到初始状态。 比如：隐藏获胜信息、重置下棋次数、清空棋盘等等。
   (1) 获取到重新开始按钮（#restart），并绑定点击事件。
   (2) 在点击事件中，重置游戏数据。
   (3) 隐藏获胜信息、清空棋盘、移除单元格点击事件、重新给单元格绑定点击事件。
   (4) 重置下棋次数、重置默认玩家为 x、重置下棋提示为 x。
5. 优化重新游戏功能：
   原来，下棋分为：1 第一次游戏 2 重新开始游戏。 现在，将第一次游戏，也看做是“重新开始游戏”，就可以去掉第一次游戏时重复的初始化操作了。
   (1) 将重新开始按钮的事件处理程序修改为：函数声明形式（startGame）。
   (2) 直接调用函数（startGame），来开始游戏。
   (3) 移除变量 steps、currentPlayer 的默认值，并添加明确的类型注解。
   (4) 移除给单元格绑定事件的代码。

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


#### 特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  Gitee 官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解 Gitee 上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是 Gitee 最有价值开源项目，是综合评定出的优秀开源项目
5.  Gitee 官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  Gitee 封面人物是一档用来展示 Gitee 会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
