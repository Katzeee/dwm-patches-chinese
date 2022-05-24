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

## bar height

https://dwm.suckless.org/patches/bar_height/

- 功能简介

  更改bar的高度

- 使用方法

  ```diff
  +static const int user_bh            = 0;        /* 0 means that dwm will calculate bar height, >= 1 means dwm will user_bh as bar height */
  ```
 更改user_bh，0表示和之前一样，大于等于1表示按照user_bh作为bar的高度。

## barconfig

https://dwm.suckless.org/patches/barconfig/

- 功能简介

  自定义bar上各标签的位置

- 使用方法

  ```diff
  +static const char *barlayout        = "tln|s";
  ```
  l：布局指示，即`[]=`，`[M]`等

  n：窗口名称

  s：状态栏，用`xsetroot`设置的

  t：标签指示，即1-9

  |：分隔符，该分隔符左边的左对齐，右边的靠右对齐

## barpadding

https://dwm.suckless.org/patches/barpadding/

- 功能简介

  使bar的水平和垂直方向有间隙，而不是紧贴屏幕边缘。

- 使用方法

  ```diff
  +static const int vertpad            = 10;       /* vertical padding of bar */
  +static const int sidepad            = 10;       /* horizontal padding of bar */
  ```
  vertpad表示垂直方向，sidepad表示水平方向。

## bartabgroups

https://dwm.suckless.org/patches/bartabgroups/

- 功能简介

  在tile模式下将bar上各client的标题按照左右分割进行展示，在float和monocle模式下只展示一个标题。用户自定义模式，如grid模式表现和tile类似。还增加了一个指示符用于指示该client在那些tag上出现。还可以更改tag指示的排列，如改为3x3的网格形式，不是1x9平铺。

- 使用方法

  ```diff
  @@ -16,6 +16,8 @@ static const char *colors[][3]      = {
 	/*               fg         bg         border   */
 	[SchemeNorm] = { col_gray3, col_gray1, col_gray2 },
 	[SchemeSel]  = { col_gray4, col_cyan,  col_cyan  },
  +	[SchemeTabActive]  = { col_gray2, col_gray3,  col_gray2 },
  +	[SchemeTabInactive]  = { col_gray1, col_gray3,  col_gray1 }
  };
  
  /* tagging */
  @@ -37,6 +39,15 @@ static const int nmaster     = 1;    /* number of clients in master area */
  static const int resizehints = 1;    /* 1 means respect size hints in tiled resizals */
  static const int lockfullscreen = 1; /* 1 will force focus on the fullscreen window */
  
  +/* Bartabgroups properties */
  +#define BARTAB_BORDERS 1       // 0 = off, 1 = on
  +#define BARTAB_BOTTOMBORDER 1  // 0 = off, 1 = on
  +#define BARTAB_TAGSINDICATOR 1 // 0 = off, 1 = on if >1 client/view tag, 2 = always on
  +#define BARTAB_TAGSPX 5        // 指示tag的小格子的像素大小
  +#define BARTAB_TAGSROWS 3      // 指示tag的小格子排多少行
  +static void (*bartabmonfns[])(Monitor *) = { monocle /* , 与monocle类似的自定义layout */ };
  +static void (*bartabfloatfns[])(Monitor *) = { NULL /* , 与float类似的自定义layout */ };
  ```
  更改以上这些定义的值可以调整该patch的效果，未设置的自定义layout应该表现都和tile类似。

## bidi(Bidirectional Text)

https://dwm.suckless.org/patches/bidi/

- 功能简介

  添加了对从右向左书写语言的支持

- 使用方法

  直接使用

## blanktags

- 功能简介
 
  将tag指示变为小方块，取消了1-9的数字指示，并且不显示没有client的tag（虽然不显示，但依然占位）

- 使用方法

  直接使用

## bottomstack

https://dwm.suckless.org/patches/bottomstack/

- 功能简介

  增加两种布局，让新client出现在master的下面。

  ```
  bstack        (TTT)       bstackhoriz   (===)
  +-----------------+       +-----------------+
  |                 |       |                 |
  |                 |       |                 |
  |                 |       |                 |
  +-----+-----+-----+       +-----------------+
  |     |     |     |       +-----------------+
  |     |     |     |       +-----------------+
  +-----+-----+-----+       +-----------------+
  ```

- 使用方法

  bstack [Alt]+[u], bstackhoriz [Alt]+[o]。

## canfocusfloating

https://dwm.suckless.org/patches/canfocusfloating/

- 功能简介

  可选择是否focus到floating client上，如开启则所有floating client将被跳过（MODKEY+j/k）无法focus。

- 使用方法

  ```diff
  +  { MODKEY,                       XK_s,      togglecanfocusfloating,   {0} },
  ```
  使用togglecanfocusfloating开启/关闭该功能。

## canfocusrule

https://dwm.suckless.org/patches/canfocusrule/

- 功能简介

  为某窗口设置rule使其永远无法被focus，对tray可能一类的软件可能很实用。

- 使用方法

  ```diff
  @@ -26,9 +26,9 @@ static const Rule rules[] = {
 	 *	WM_CLASS(STRING) = instance, class
 	 *	WM_NAME(STRING) = title
 	 */
  -	/* class      instance    title       tags mask     isfloating   monitor */
  -	{ "Gimp",     NULL,       NULL,       0,            1,           -1 },
  -	{ "Firefox",  NULL,       NULL,       1 << 8,       0,           -1 },
  +	/* class      instance    title       tags mask     isfloating canfocus   monitor */
  +	{ "Gimp",     NULL,       NULL,       0,            1,         1,         -1 },
  +	{ "Firefox",  NULL,       NULL,       1 << 8,       0,         1,         -1 },
  };
  ```
  更改rule数组，canfocus为0表示不可focus。

## center

https://dwm.suckless.org/patches/center/

- 功能简介

  为某窗口设置rule使其永远居中。

- 使用方法

  ```diff
  @@ -26,9 +26,9 @@ static const Rule rules[] = {
  *	WM_CLASS(STRING) = instance, class
  *	WM_NAME(STRING) = title
  */
  -	/* class      instance    title       tags mask     isfloating   monitor */
  -	{ "Gimp",     NULL,       NULL,       0,            1,           -1 },
  -	{ "Firefox",  NULL,       NULL,       1 << 8,       0,           -1 },
  +	/* class      instance    title       tags mask     iscentered   isfloating   monitor */
  +	{ "Gimp",     NULL,       NULL,       0,            0,           1,           -1 },
  +	{ "Firefox",  NULL,       NULL,       1 << 8,       0,           0,           -1 },
  };
  ```
  更改rule数组，在iscentered的位置给1表示居中。

## center first window

https://dwm.suckless.org/patches/center_first_window/

- 功能简介

  若整个tag内只有一个client则将其center，可通过rule设置哪个窗口被center。
  ```
  +-----------------------------+         +-----------------------------+
  |                             |         | +------------+ +----------+ |
  |                             |         | |            | |          | |
  |                             |         | |            | |          | |
  |       +-------------+       |         | |            | |          | |
  |       |    Single   |       |         | |  Terminal  | | Terminal | |
  |       |   Terminal  |       |         | |  Window 1  | | Window 2 | |
  |       |    Window   |       |         | |            | |          | |
  |       +-------------+       |         | |            | |          | |
  |                             |         | |            | |          | |
  |                             |         | |            | |          | |
  |                             |         | +------------+ +----------+ |
  +-----------------------------+         +-----------------------------+
  ```
  适用于很大的屏幕，一个terminal可能需要看到屏幕的左上角很不方便。

- 使用方法

  ```diff
  @@ -26,9 +26,10 @@ static const Rule rules[] = {
 	 *	WM_CLASS(STRING) = instance, class
 	 *	WM_NAME(STRING) = title
 	 */
  -	/* class      instance    title       tags mask     isfloating   monitor */
  -	{ "Gimp",     NULL,       NULL,       0,            1,           -1 },
  -	{ "Firefox",  NULL,       NULL,       1 << 8,       0,           -1 },
  +	/* class      	     instance    title    tags mask     isfloating   CenterThisWindow?     monitor */
  +	{ "st",              NULL,       NULL,    0,            0,     	     1,		           -1 },
  +	{ "Gimp",            NULL,       NULL,    0,            1,           0,                    -1 },
  +	{ "Firefox",         NULL,       NULL,    1 << 8,       0,           0,                    -1 },
  };
  ```
  更改rule数组，CenterThisWindow表示该client启用此patch的功能。

## centeredmaster

https://dwm.suckless.org/patches/centeredmaster/

- 功能简介

  增加了两种布局centeredmaster，centeredfloatingmaster。效果如下
  ```
  centeredmaster
  +------------------------------+       +------------------------------+
  |+--------++--------++--------+|       |+--------++--------++--------+|
  ||        ||        ||        ||       ||        ||        ||        ||
  ||        ||        ||        ||       ||        ||   M1   ||        ||
  ||        ||        ||        ||       ||        ||        ||        ||
  ||  S2    ||   M    ||   S1   ||       ||        |+--------+|        ||
  ||        ||        ||        ||       ||        |+--------+|        ||
  ||        ||        ||        ||       ||        ||        ||        ||
  ||        ||        ||        ||       ||        ||   M2   ||        ||
  ||        ||        ||        ||       ||        ||        ||        ||
  |+--------++--------++--------+|       |+--------++--------++--------+|
  +------------------------------+       +------------------------------+
  centeredfloatingmaster（仅master窗口浮动在中央）
  +------------------------------+       +------------------------------+
  |+--------++--------++--------+|       |+--------++--------++--------+|
  ||        ||        ||        ||       ||        ||        ||        ||
  ||    +------------------+    ||       ||    +--------++--------+    ||
  ||    |                  |    ||       ||    |        ||        |    ||
  ||    |                  |    ||       ||    |        ||        |    ||
  ||    |        M         |    ||       ||    |   M1   ||   M2   |    ||
  ||    |                  |    ||       ||    |        ||        |    ||
  ||    +------------------+    ||       ||    +--------++--------+    ||
  ||        ||        ||        ||       ||        ||        ||        ||
  |+--------++--------++--------+|       |+--------++--------++--------+|
  +------------------------------+       +------------------------------+
  ```
  
- 使用方法

  ```diff
  @@ -39,6 +39,8 @@ static const Layout layouts[] = {
 	{ "[]=",      tile },    /* first entry is default */
 	{ "><>",      NULL },    /* no layout function means floating behavior */
 	{ "[M]",      monocle },
  +	{ "|M|",      centeredmaster },
  +	{ ">M>",      centeredfloatingmaster },
  };

  +	{ MODKEY,                       XK_u,      setlayout,      {.v = &layouts[3]} },
  +	{ MODKEY,                       XK_o,      setlayout,      {.v = &layouts[4]} },
  ```
  通过快捷键切换布局。
  
## centeredwindowname

https://dwm.suckless.org/patches/centeredwindowname/

- 功能介绍

  将client的名称居中显示而不是靠在显示在bar上。

- 使用方法

  直接使用

## centertitle

https://dwm.suckless.org/patches/centretitle/

- 功能介绍

  将client的名称居中显示而不是靠在显示在bar上。与上面的补丁功能类似，区别不明，未测试。

- 使用方法

  直接使用

## cfacts

https://dwm.suckless.org/patches/cfacts/

- 功能介绍

  可以调整client的高度（默认只能左右）
  ```
  +---------------------+
  |          |   0.5    |
  |   1.0    +----------+
  +----------+          |
  |          |   1.0    |
  |          +----------+
  |   2.0    |          |
  |          |   1.0    |
  +----------+----------+
  ```

  还提供了三种基于cfacts的layout。bottomstack，centeredmaster和deck。

- 使用方法

  ```diff
  +	{ MODKEY|ShiftMask,             XK_h,      setcfact,       {.f = +0.25} },
  +	{ MODKEY|ShiftMask,             XK_l,      setcfact,       {.f = -0.25} },
  +	{ MODKEY|ShiftMask,             XK_o,      setcfact,       {.f =  0.00} },
  ```
  从上到下依次是变高，变低，复原。

## clientindicators

https://dwm.suckless.org/patches/clientindicators/

- 功能简介

  原始的dwm只有小矩形指示该tag是否有client，该patch可以显示client的数量。

  dwm-clientindicators-6.2.diff 为该补丁

  dwm-clientindicatorshidevacant-6.2.diff 为该补丁+hidevacant补丁

- 使用方法

  直接使用
  
## clientmonoclesymbol

https://dwm.suckless.org/patches/clientmonoclesymbol/

- 功能简介

  将monocle layout的client数量指示标改为自定义的图标，即`[1]`，`[2]`之类的可自定义。

- 使用方法

  ```diff
  +/* 当clients数量大于设置的图标数量时，使用最后一个 */
  +static const char *monocles[] = { "[1]", "[2]", "[3]", "[4]", "[5]", "[6]", "[7]", "[8]", "[9]", "[9+]" };
  ```
  设置monocles数组以改变图标。

## clientopacity

https://dwm.suckless.org/patches/clientopacity/

- 功能简介

  可以更改client的透明度。

- 使用方法

  ```diff
  +static const double defaultopacity  = 0.75; // 默认透明度

  @@ -26,9 +27,10 @@ static const Rule rules[] = {
 	*	WM_CLASS(STRING) = instance, class
 	*	WM_NAME(STRING) = title
 	*/
  -	/* class      instance    title       tags mask     isfloating   monitor */
  -	{ "Gimp",     NULL,       NULL,       0,            1,           -1 },
  -	{ "Firefox",  NULL,       NULL,       1 << 8,       0,           -1 },
  +	/* class      instance    title       tags mask     isfloating	 opacity	monitor */
  +	{ "Gimp",     NULL,       NULL,       0,            1,           1.0,		-1 },
  +	{ "Firefox",  NULL,       NULL,       1 << 8,       0,           1.0,		-1 },
  +	{ "St",	      NULL,       NULL,       0,            0,           defaultopacity, -1},

  +	{ MODKEY|ShiftMask,		XK_KP_Add, changeopacity,	{.f = +0.1}},
  +	{ MODKEY|ShiftMask,		XK_KP_Subtract, changeopacity,  {.f = -0.1}},
  ```
  defaultopacity为默认透明度，可以通过rule给窗口单独设置透明度，通过快捷键也可调整focus窗口的透明度。

## clients per tag

https://dwm.suckless.org/patches/clientspertag/

- 功能简介

  可以设置一个tag中最多可以看见的client数量，多余的会和monocle一样被压在下面，也可理解为monocle布局，但是一层可以有多个client。（该patch最新版本时2009年的，不知是否还可使用）

  ```
  +-----------------------+  +-----------------------+
  | -1/3                  |  |  2/3                  |
  +-----------+-----------+  +-----------+-----------+
  |           |           |  |           |           |
  |           |     2     |  |           |           |
  |           |           |  |           |           |
  |     1     +-----------+  |     1     |     2     |
  |           |           |  |           |           |
  |           |     3     |  |           |           |
  |           |           |  |           |           |
  +-----------+-----------+  +-----------+-----------+
            cpt=-1                     cpt=2
  ```

- 使用方法

  ```diff
  +static int cpt = -1; //-1显示所有client，0只显示floating client，其他为显示个数

  static Key keys[] = {
	/* modifier      key        function        argument */
	...
	+ { MODKEY,        XK_q,      clientspertag,  {.v="2"} },
	+ { MODKEY,        XK_a,      clientspertag,  {.v="^3"} },
  };
  ```
  .v=2表示给cpt赋值为2，^3表示将cpt的值在3和-1之间切换，即按一次cpt为3，再按一次就切换回-1。

## cmdcustomize(customise dwm through command line)

https://dwm.suckless.org/patches/cmdcustomize/

- 功能简介

  dwm默认只能从config.h中设置主题颜色，每次设置完需要重新编译，该补丁可以在启动dwm时使用命令行参数设置颜色。

- 使用方法

  - fn：dwm字体
  - df：dmenu字体
  - nb：普通背景颜色
  - nf：普通前景颜色
  - sb：选中背景颜色 
  - sf：选中前景颜色
  - dnb：dmenu普通背景颜色 
  - dnf：dmenu普通前景颜色
  - dsb：dmenu选中背景颜色
  - dsf：dmenu选中前景颜色

## colemak_keys

https://dwm.suckless.org/patches/colemak_keys/

- 功能简介

  将原快捷键布局改为符合colemak键盘布局的快捷键键位。

- 使用方法
  
  直接使用

## colorbar

https://dwm.suckless.org/patches/colorbar/

- 功能简介

  可以自定义bar的各部件的颜色。

- 使用方法

  ```diff
  [SchemeSel]  = { col_gray4, col_cyan,  col_cyan  },
  +	[SchemeStatus]  = { col_gray3, col_gray1,  "#000000"  }, // Statusbar right {文本，背景，未使用但不能为空}
  +	[SchemeTagsSel]  = { col_gray4, col_cyan,  "#000000"  }, // Tagbar left 选中 {文本，背景，未使用但不能为空}
  +    [SchemeTagsNorm]  = { col_gray3, col_gray1,  "#000000"  }, // Tagbar left 未选中 {文本，背景，未使用但不能为空}
  +    [SchemeInfoSel]  = { col_gray4, col_cyan,  "#000000"  }, // infobar middle  选中 {文本，背景，未使用但不能为空}
  +    [SchemeInfoNorm]  = { col_gray3, col_gray1,  "#000000"  }, // infobar middle  未选中 {文本，背景，未使用但不能为空}
  ```

## columngaps

https://dwm.suckless.org/patches/columngaps/

- 功能简介

  该补丁为column layout添加了间隙吗，如同tilegaps给tile布局添加间隙一样。该补丁内置column layout。

- 使用方法

  ```diff
  +static const unsigned int gappx     = 12;       /* 间隙的大小 */
  +	{ MODKEY,                       XK_c,      setlayout,      {.v = &layouts[3]} },
  ```
  提供快捷键切换至column layout。

## columns

https://dwm.suckless.org/patches/columns/

- 功能简介

  提供column layout。将整个tag内的布局按列平均排布，始终有nmater+1列，最后一列与tile布局类似，是叠起来的布局。可以理解为将tile布局的master位置按列又拆了几块。

- 使用方法

  与columngaps相同，只是没有client之间的gap。

## combo

https://dwm.suckless.org/patches/combo/

- 功能简介

  提供“按住”而不是切换的方式同时查看多个tag，dwm默认操作是MODKEY+CTRL+(1-9)同时查看选中的tag，再按一次可以取消对某tag的选中。

- 使用方法

  按住MODKEY并同时按住1、3可以同时查看1、3tag中的内容。

## cool autostart

https://dwm.suckless.org/patches/cool_autostart/

- 功能简介

  使dwm执行一些命令，并在退出dwm之后关闭由该该命令所产生的所有进程。（可以用其打开vpn之类的软件）

- 使用方法

  ```diff
  +static const char *const autostart[] = {
  +	"st", NULL,
  +	NULL /* terminate */
  +};
  +
  ```
  在autostart数组中写入需要执行的命令，每条命令以NULL结尾，所有命令之后也以NULL结尾。

## cropwindows

https://dwm.suckless.org/patches/cropwindows/

- 功能简介

  创建现有窗口的裁剪视图，只显示其中的一部分，通常是为了从框架不好的视频或程序和设计糟糕的网站中回收屏幕空间。

- 使用方法

  ```diff
  +{ ClkClientWin, MODKEY|ShiftMask, Button1, movemouse,   {.i = 1} },
  +{ ClkClientWin, MODKEY|ShiftMask, Button3, resizemouse, {.i = 1} },
  ```
  MODKEY+SHIFT+鼠标左键可以创建一个裁剪窗口，MODKEY+SHIFT+鼠标右键可以移动该窗口里的内容。

## current_desktop

https://dwm.suckless.org/patches/current_desktop/

- 功能简介

  将root上的_NET_NUMBER_OF_DESKTOPS和_NET_CURRENT_DESKTOP设置为适当的值。请注意，这些值的“适当”作为`xprop -root`输出没有意义，因为dwm按位使用它们，但xprop以十进制显示它们。如果您选择了桌面1和3，则值为0b1010，但xprop将其显示为10。作者提到他有一个脚本使用了该特性，我理解这样可以同时将多个桌面（DESKTOP）作为一个桌面进行处理。

- 使用方法

  直接使用

## cursorwarp

https://dwm.suckless.org/patches/cursorwarp/

- 功能简介

  使切换focus或monitor的时候将鼠标移至屏幕中间。

- 使用方法

  直接使用

  dwm-cursorwarp-20210222-61bb8b2.diff为默认版本。

  dwm-cursorwarp-mononly-20210222-61bb8b2.diff仅在更换显示器时移动鼠标。

  dwm-cursorwarp-stackonly-20210222-61bb8b2.diff仅在切换focus窗口时。

## cyclelayouts

https://dwm.suckless.org/patches/cyclelayouts/

- 功能简介

  提供快捷键循环窗口layout，dwm默认只可以在两个layout之间来回换。

- 使用方法

  ```diff
  @@ -41,6 +41,7 @@ static const Layout layouts[] = {
 	{ "[]=",      tile },    /* first entry is default */
 	{ "><>",      NULL },    /* no layout function means floating behavior */
 	{ "[M]",      monocle },
  +	{ NULL,       NULL },
  };

  +	{ MODKEY|ControlMask,		XK_comma,  cyclelayout,    {.i = -1 } },
  +	{ MODKEY|ControlMask,   XK_period, cyclelayout,    {.i = +1 } },
  ```
  最后一个布局需要设置为NULL, NULL，使用提供的快捷键可以在布局之间循环。

