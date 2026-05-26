============================================================
  飞行雪绒历险记 — 躲避弹幕生存游戏
============================================================

  纯 HTML/CSS/JS 实现，双击 飞行雪绒历险记.html 即可运行。


【目录结构】

  飞行雪绒历险记（网页）/
  ├── 飞行雪绒历险记.html   游戏主文件
  ├── character/             角色图片
  ├── skill_character/       大招效果图
  └── README.txt


【操作说明】

  W A S D / 方向键   惯性移动（松手保持运动，按键匀加速）
  空格                大招：清除全部弹幕 + 积分+10（冷却5s）
  Q                   消耗10积分，随机回复20~50 HP（冷却5s）
  E                   长按：弹幕减速70% + 计时减速（每秒-1分）
  F                   最终得分>=500时召唤传送门，靠近后按F结算
  ESC                 暂停 / 继续
  R                   重置回选人界面


【游戏规则】

  -- 生命与计时 --
  - 100点生命值，受伤扣除弹幕上标注的伤害值（0~10），归零失败
  - 180秒倒计时，归零存活成功
  - 受伤后1秒无敌闪烁
  - 每受伤1 HP，场上弹幕上限+1

  -- 弹幕 --
  - 红/黄/蓝/紫/粉 五种颜色，空心环形，红色数字标注伤害值
  - 碰到边界反弹并加速5%，基础上限25颗
  - 大招期间暂停生成，游戏结束后弹幕冻结

  -- 积分球 --
  - 绿色实心圆球，分值1~10（越大分越高），触碰收集
  - 场上总分保持50~100，总球数8~20
  - 吃掉一个后随机生成0~2个新球

  -- 结算 --
  - 最终得分 = 积分 x 剩余HP百分比
  - >=500分可召唤传送门提前结算
  - >=1005分触发神秘彩蛋


【自定义配置】

  -- 修改角色图片 --
  编辑 HTML 文件中 CHARACTER_IMAGE_PATHS 数组（约第127行）：
    const CHARACTER_IMAGE_PATHS = [
      './character/角色1.png',
      './character/角色2.png',
      // 添加更多...
    ];
  也可在选人界面点击「追加角色图」手动加载。

  -- 修改大招效果图 --
  编辑 SKILL_IMAGE_PATHS 数组（约第118行）：
    const SKILL_IMAGE_PATHS = [
      './skill_character/大招效果图1.png',
      './skill_character/大招效果图2.png',
      // 添加更多...
    ];

  -- 调整游戏参数 --
  所有可调参数在 <script> 开头附近：
    GAME_DURATION       游戏时长(秒)        默认 180
    SKILL_COOLDOWN      大招冷却(秒)        默认 5
    Q_COOLDOWN          Q技能冷却(秒)       默认 5
    Q_HEAL_MIN/MAX      Q技能回复范围       默认 20~50
    E_BULLET_SLOW       E技能弹幕减速比例   默认 0.3
    BASE_MAX_BULLETS    基础弹幕上限        默认 25
    ORB_SUM_MIN/MAX     积分球总分范围      默认 50~100
    ORB_COUNT_MIN/MAX   积分球数量范围      默认 8~20
    SKILL_IMG_SCALE     大招图片缩放比例    默认 0.45


【换电脑使用】

  把整个文件夹（HTML + character/ + skill_character/）一起拷贝，
  角色图和大招图已预配置，无需重新手动加载。
  打开后角色自动选中，直接点「开始游戏」即可。


【打包为 EXE】

  方法1（推荐）：NW.js (https://nwjs.io/)
    1. 下载 NW.js SDK
    2. 在游戏目录创建 package.json:
       {
         "name": "飞行雪绒历险记",
         "main": "飞行雪绒历险记.html",
         "window": { "width": 820, "height": 660 }
       }
    3. 将文件夹拖到 nw.exe 上即可运行
    4. 用 Enigma Virtual Box 打包为单个 exe

  方法2：Electron (https://www.electronjs.org/)
  方法3：DecSoft HTML Compiler 一键编译
