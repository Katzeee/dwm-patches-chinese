## accessnthmonitor

https://dwm.suckless.org/patches/accessnthmonitor/ 

- 功能简介

  功能如其名，到达第n个显示器，用于在多显示器环境中直接切换。

- 使用方法

  ```diff
  +        { ALTMOD,                       KEY,      focusnthmon,    {.i  = TAG } }, \
  +        { ALTMOD|ShiftMask,             KEY,      tagnthmon,      {.i  = TAG } },
  ```
  
  使用focusnthmon切换到第n个monitor，使用tagnthmon将当前focus的窗口移至第n个显示器。

## activetagindicatorbar

https://dwm.suckless.org/patches/activetagindicatorbar/

- 功能简介

  此补丁将指示Client是否被使用的矩形标记更改为tag数字上方的条状标记。使用时需注意tag的字体在顶部留出足够的空间。 

- 使用方法

  直接使用

## actualfullscreen

https://dwm.suckless.org/patches/actualfullscreen/

- 功能简介

  切换至真正的全屏而不是通过开关bar切换全屏（两者的区别待补充）

- 使用方法

  ```diff
  +	{ MODKEY|ShiftMask,             XK_f,      togglefullscr,  {0} },
  ```

  使用togglefullscr进入/退出全屏模式

## adjacenttag 

https://dwm.suckless.org/patches/adjacenttag/

- 功能简介

  用于快速在相邻的tag之间切换，使用`skipvacant`版本可以跳过空闲标签。

- 使用方法

  ```diff
  +	{ MODKEY,                       XK_Right,  viewnext,       {0} },
  +	{ MODKEY,                       XK_Left,   viewprev,       {0} },
  +	{ MODKEY|ShiftMask,             XK_Right,  tagtonext,      {0} },
  +	{ MODKEY|ShiftMask,             XK_Left,   tagtoprev,      {0} },
  ```

  使用viewnext切换至右边的tag，viewprev左边，使用tagtonext，将当前focus的client切换到右边的tag，tagtoprev，将当前focus的client切换到左边的tag。

## alpha 

https://dwm.suckless.org/patches/alpha/

- 功能简介

  透明的bar

- 使用方法

  直接使用

## alternativetags 

https://dwm.suckless.org/patches/alternativetags/

- 功能简介

  允许在运行过程中更改bar上各tag的标识符，不用的时候可以为设置好的图案，切换时可以换回数字更快操作，但只能设置两组进行切换。

- 使用方法

  ```diff
  @@ -20,6 +20,8 @@ static const char *colors[][3]      = {
  /* tagging */
  static const char *tags[] = { "1", "2", "3", "4", "5", "6", "7", "8", "9" };
  +static const char *tagsalt[] = { "1", "2", "3", "4", "5", "6", "7", "8", "9" };
  +static const int momentaryalttags = 0; /* 1 means alttags will show only when key is held down*/
  
  @@ -85,6 +87,7 @@ static Key keys[] = {
    { MODKEY|ShiftMask,             XK_period, tagmon,         {.i = +1 } },
  +	{ MODKEY,                       XK_n,      togglealttag,   {0} },
  ```
  
  在tagsalt和tags中设置想要切换的图标，togglealttag可以切换两组tag的图案，若将momentaryalttags设置为1，则在按住快捷键时显示切换的图案，而不是按下切换。

## alttagsdecoration

https://dwm.suckless.org/patches/alttagsdecoration/

- 功能简介

  将有client的tag标识从每个tag左上角的小矩形换为自定义图标。

- 使用方法

  ```diff
  static const char *tags[] = { "1", "2", "3", "4", "5", "6", "7", "8", "9" };
  +static const char *alttags[] = { "<01>", "<02>", "<03>", "<04>", "<05>" };
  ```

  在alttags中设置想要的图案，当该tag有client的时候，tag标识则会更改。

## alwayscenter

https://dwm.suckless.org/patches/alwayscenter/

- 功能简介

  所有floating的窗口将被居中，与`center`补丁功能类似，但不需要规则。

- 使用方法

  直接使用

## alwaysfullscreen

https://dwm.suckless.org/patches/alwaysfullscreen/

- 功能简介

  当调用focusstack函数时，focus不会从fullscreen的client上移至切换的窗口。该补丁以及被写入`67d76bdc6810`版本之后的dwm，因此仅版本靠前的dwm需要此补丁。

- 使用方法

  直接使用

## alwaysontop

https://dwm.suckless.org/patches/alwaysontop/

- 功能简介

  使选定的floating窗口用于位于最上层。

- 使用方法

  ```diff
  +	{ MODKEY|ShiftMask,             XK_space,  togglealwaysontop, {0} },
  ```

  togglealwaysontop将focus的窗口开启/关闭位于最上层。 


## anybar

https://dwm.suckless.org/patches/anybar/

- 功能简介

  将dwm的bar换为其他bar，如lemonbar或polybar。

- 使用方法

  ```diff
  @@ -5,6 +5,10 @@ static const unsigned int borderpx  = 1;        /* border pixel of windows */
  static const unsigned int snap      = 32;       /* snap pixel */
  static const int showbar            = 1;        /* 0 means no bar */
  static const int topbar             = 1;        /* 0 means bottom bar */
  +static const int usealtbar          = 1;        /* 1 means use non-dwm status bar */
  +static const char *altbarclass      = "Polybar"; /* Alternate bar class name */
  +static const char *alttrayname      = "tray";    /* Polybar tray instance name */
  +static const char *altbarcmd        = "$HOME/bar.sh"; /* Alternate bar launch command */
  static const char *fonts[]          = { "monospace:size=10" };
  static const char dmenufont[]       = "monospace:size=10";
  static const char col_gray1[]       = "#222222";
  ```

 showbar必须为1，usealtbar表示使用外部bar，altbarclass为外部bar的class name，alttrayname为外部tray的instance name，这两个参数可以通过`xprop`命令找到。altbarcmd为启动该bar的命令。

## aspectresize

https://dwm.suckless.org/patches/aspectresize/

- 功能简介

  按照固定纵横比的方式更改client的尺寸。

- 使用方法

  ```diff
  +	{ MODKEY|ShiftMask,             XK_j,      aspectresize,   {.i = +24} },
  +	{ MODKEY|ShiftMask,             XK_k,      aspectresize,   {.i = -24} },
  ```

  设置.i参数更改放大和缩小的速度。

## attachabove

https://dwm.suckless.org/patches/attachabove/

- 功能简介

  使新创建的client不位于master位置，而是当前窗口的前一个位置。

- 使用方法

  直接使用

##  attachaside

https://dwm.suckless.org/patches/attachaside/

- 功能简介

  使新创建的client不位于master位置，而是堆起来（右边）的位置。可能是当前tag中非浮动窗口的第一个窗口之后，待测试。

  ```
  原dwm： 
  +-----------------+-------+
  |                 |       |（N表示新窗口，P表示原窗口）
  |                 |   P   |
  |                 |       |
  |        N        +-------+
  |                 |       |
  |                 |       |
  |                 |       |
  +-----------------+-------+
  补丁后：
  +-----------------+-------+
  |                 |       |
  |                 |   N   |
  |                 |       |
  |        P        +-------+
  |                 |       |
  |                 |       |
  |                 |       |
  +-----------------+-------+
  +-----------------+-------+
  |                 |       |
  |                 |   P   |
  |                 |       |
  |                 +-------+
  |                 |       |
  |                 |   N   |
  |                 |       |
  +-----------------+-------+
  ```
  
- 使用方法

  直接使用

## attachasideandbelow

https://dwm.suckless.org/patches/attachasideandbelow/

- 功能简介

  以上两个patch的结合，具体功能待补充，功能应该与aside相同但是代码有改进，考虑了更多的“意外情况”。

- 使用方法

  直接使用

## attachbelow

https://dwm.suckless.org/patches/attachbelow/

- 功能简介

  使新创建的client不位于master位置，而是focus窗口的上一个位置。

- 使用方法

  ```diff
  +{ MODKEY,                       XK_Tab,           toggleAttachBelow,           {0} },
  ```
  可以通过快捷键来启用/关闭该功能。

## attachbottom

https://dwm.suckless.org/patches/attachbottom/

- 功能简介

  使新创建的client不位于master位置，而是整个tag中最后（最下）的位置。

- 使用方法

  直接使用

## attachdirection

https://dwm.suckless.org/patches/attachdirection/

- 功能简介 

  该补丁是1)attachabove，2)attachaside，3)attachbelow，4)attachbottom 和 5)attachtop的结合。可惜没有在源码中写出运行时更改attach方案的函数，实现起来也很简单。

- 使用方法

  ```diff
  +static const int attachdirection = 0;    /* 0 default, 1 above, 2 aside, 3 below, 4 bottom, 5 top */
  ```

  attachdirection设置为0，1，2，3，4，5分别表示新client将attach到默认，上，旁边，下，最底，最上。

## attachtop

https://dwm.suckless.org/patches/attachtop/

- 功能简介

  使新创建的client不位于master位置，而是master窗口的下一个位置，也就是右边最上的位置。当只有一个master时和attachaside功能相同。

- 使用方法
  
  直接使用

## autoresize

https://dwm.suckless.org/patches/autoresize/

- 功能简介

  正常无法调整不可见窗口的大小和位置，此patch使其可以被调整。（不确定：此处的不可见窗口是指其他tag中的窗口，所以意思是调整一个tag布局的时候同时也会改变其他窗口的）。

- 使用方法

  直接使用

## autostart

https://dwm.suckless.org/patches/autostart/

- 功能简介

  这个补丁将在dwm进入主循环运行之前运行`~/.dwm/autostart_blocking.sh`和`~/.dwm/autostart.sh &`，然后才启动dwm。可以省略其中一个或两个文件。
  上面列出的文件分别在目录`$XDG_DATA_HOME/DWM`、`$HOME/.local/Share/DWM`和`$HOME/.dwm`中查找。将会在最先找到的目录中运行脚本，即使该目录下没有脚本。

- 使用方法

  直接使用，将脚本文件放入`~/.dwm`下，同时确保没有上面提到的另两个目录。同时注意若`~/.dwm/autostart_blocking.sh`无法执行完毕，则将卡死。

## awesomebar

https://dwm.suckless.org/patches/awesomebar/

- 功能简介

  - 将在bar上显示tag中所有的client名称，而不只是focus的那个
  - 点击bar上的client名称可以切换focus
  - 点击focus的client名称可以隐藏该client
  - 点击隐藏的client名称会将其取消隐藏并切换至focus
  - 可以快捷键访问循环访问非隐藏窗口或全部窗口

- 使用方法

  ```diff
    { MODKEY,                       XK_b,      togglebar,      {0} },
  -	{ MODKEY,                       XK_j,      focusstack,     {.i = +1 } },
  -	{ MODKEY,                       XK_k,      focusstack,     {.i = -1 } },
  +	{ MODKEY,                       XK_j,      focusstackvis,  {.i = +1 } },
  +	{ MODKEY,                       XK_k,      focusstackvis,  {.i = -1 } },
  +	{ MODKEY|ShiftMask,             XK_j,      focusstackhid,  {.i = +1 } },
  +	{ MODKEY|ShiftMask,             XK_k,      focusstackhid,  {.i = -1 } },
    { MODKEY,                       XK_i,      incnmaster,     {.i = +1 } },
  +	{ MODKEY,                       XK_s,      show,           {0} },
  +	{ MODKEY,                       XK_h,      hide,           {0} },
   ```

  MODKEY+j和MODKEY+k现在用于循环访问非隐藏窗口，MODKEY+SHIFT可以循环访问所有窗口，包括隐藏窗口。MODKEY+h和s用于隐藏和显示当前focus的窗口。
   
  在打补丁时我发现可能因为该patch基于较为古老的dwm所写，新的dwm中focusstack的代码进行了改进

  因此对于diff文件中的
  ```diff
  +void
  +focusstack(int inc, int hid)
  {
 	Client *c = NULL, *i;
 
  -	if (!selmon->sel) // dwm6.3源码中已经删除了该行
  +	if (!selmon->sel && !hid)
 		return;
  ```
  这部分的代码应该改为
  ```diff
  Client *c = NULL, *i;
   
  - if (!selmon->sel || (selmon->sel->isfullscreen && lockfullscreen)) // dwm6.3
  + if ((!selmon->sel && !hid) || (selmon->sel && selmon->sel->isfullscreen && lockfullscreen))
   	return;
  ```
  同时我还编写了一个函数用于使当前tag中所有窗口全部取消隐藏的函数。也可将其加入dwm.c并在config.h中为其设置快捷键。
  ```c
  // dwm.c
  void
  showall(const Arg *arg)
  {
    Client *c = NULL;
    selmon->hidsel = 0;
    for (c = selmon->clients; c ; c = c->next) {
      if (ISVISIBLE(c)) // the client in current tag
        showwin(c);
    }
    if (!selmon->sel) { // if no focus, select one to focus
      for (c = selmon->clients; c && !ISVISIBLE(c); c = c->next);
      if (c)
        focus(c);
    }
    restack(selmon);
  }
  // config.h
  { MODKEY|ShiftMask,             XK_s,      showall,        {0} },
  ```

## azerty

https://dwm.suckless.org/patches/azerty/

- 功能简介

  将原快捷键布局改为符合azerty键盘布局的快捷键键位。

- 使用方法

  直接使用