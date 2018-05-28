# 基于ARC EM处理器的车载语音控制系统
## 第一章 方案论证
### 1.1项目概述
伴随着人民生活水平的提高，汽车的使用正在逐渐普及。在汽车数量增长的同时，人们对汽车的使用也提出了安全性、舒适性、便捷性等多方面的需求。为了满足用户的这些需求，提髙市场竞争力，国内外汽车厂商不断推出或者升级车载设备，尤其是车载多媒体系统和自动驾驶技术的加入，为驾乘人员提供了丰富的车载娱乐生活，提髙了驾乘体验。传统的车载设备大多需要用户采用触碰、按压或旋转的方式进行控制和交互。这种交互方式需要驾乘人员的手部和眼部的参与和协作，这与需要高度专注并且手部操作频繁的驾驶行为产生了直接的冲突。随着车载电子设备的逐渐增多，驾驶员所要进行的操作也越来越复杂，驾驶安全也因此受到影响。语音作为人类信息产生和交流的重要方式之一，具有高效，简单，便捷的特点，使用语音命令作为人车交互的接口，可以解放驾驶人员的双手，驾驶员仅需说出特定的控制指令，不必移动视线或进行其他的肢体动作，即可控制车载设备，这样既可增添驾驶乐趣，也可提髙行车安全性。因此很多汽车厂商逐渐在车载设备上开放了语音识别接口，实现用语音对车载设备的控制和交互。
我们计划利用带有DSP模块的ARC EM DSP处理器实现语音识别功能，通过不同语音指令完成对车内常见操作的控制，增添驾驶乐趣，提高驾驶安全性。
预期操作者可在不同噪声环境下，发出相应语音指令，实现对车内设备的控制。例如空调调节、音乐播放、调频广播、车门开关上锁解锁、车窗升降、雨刮器启动停止、座椅高度调节等基本功能。后期根据情况可扩展导航、手机电话联网等功能。
我们通过对市场需求和多篇期刊论文的调研以及MATLAB仿真，已得到实现语音识别的基本算法，并准备将其与神经算法相结合，提升语音识别的速度和准确性。
### 1.2资源评估
芯片的选择需要充分考虑系统需要，本系统的主要功能是：通过语音指令完成对车内设备的控制。其中的语音识别功能需要对音频数据进行大量复杂运算，对处理器的计算能力提出了挑战。为了满足实时性要求，需要选择一款带DSP的ARC EM处理器。带DSP的ARC EM处理器具有以下资源
   
   采用三级流水  
   ARCv2DSP ISA增加了超过100条DSP指令  
   定点、矢量和SIMD DSP支持  
   高能效的统一32×32MLU/MAC单元  
   高度可配置的DSP和处理器功能   
   MetaWare C/C++编译器，支持DSP编程  
   功能丰富的DSP软件库，提供便捷的算法编程  
   可选的硬件除法器   
   高达1.77DMIPS/MHz和3.41CoreMark/MHz的性能   
   支持APEX处理器扩展套件的加速  
   JTAG调试界面    
   此外，系统还需要增加一些外设，包括前端音频模块和触摸屏模块。音频负责将音频模拟信号转换为需要的数字信号，我们选用WM8731音频模块，此模块不仅可实现MIC直接输入还满足蓝牙远程输入。当然实际应用中由于成本要求，
 我们可以自行设计AD转换模块以降低成本。触摸屏模块负责显示和手动输入，我们选择常用的TFT液晶触摸屏。
  ### 1.3预期结果
  项目预期结果为，当驾驶员在发出语音指令后，汽车各个设备可以迅速做出准确反应。由于汽车系统比较庞大复杂，初期我们将汽车的一些具体操作做如下模拟：开窗LED1灯亮，关窗LED2灯亮；开门LED3灯亮，关门LED4灯亮；空调热风LED5亮，空调冷风LED6亮；音乐开LED7亮；雨刮器开LED8亮。后期会根据时间做出更具显示度的成品，例如可以做成语音遥控汽车。
要求在汽车正常行驶的背景噪声下，对于语音指令的识别准确率不低于80%。
### 1.4项目实施评估
项目实施计划如下：   
2018.1—2018.3 项目方案及系统设计   
2018.3—2018.4 语音识别算法研究与编程实现   
2018.4—2018.5 搭建硬件电路与系统实现   
2018.5—2018.6 调试与测试   
## 第二章 作品难点与创新
### 2.1作品难点分析
作品的主要创新点如下   
1.算法创新   
语音识别阶段采用基于神经网络的算法，较传统的DTW和HMM语音识别算法更适用于车载环境，识别速度更快，识别准确率更高   
2.硬件创新   
语音输入设备采用蓝牙输入和普通麦克输入两种模式。蓝牙输入模式的增加降低了环境噪声的影响，提高了语音输入系统的抗干扰能力  
3.设计创新   
本章对系统的难点和创新性进行了分析，主要介绍了系统在语音识别方面的困难以及在算法、硬件、设计方面的创新   
### 2.3小结
本章对系统的难点和创新性进行了分析，主要介绍了系统在语音识别方面的困难以及在算法、硬件、设计方面的创新
## 第三章 系统结构与硬件实现
### 3.1系统原理分析
该车载语音控制系统以ARC EM系列处理器作为控制器，外围电路包括MIC输入模块、蓝牙输入模块、功放和喇叭输出模块、LED显示系统及其他各类信号的采集和输出。操作者可通过触摸屏按键，使系统进入指令训练模式，处理器根据操作者的提供的训练语句完成系统的语音识别训练，训练完成，由喇叭输出模块发出语音信号，提示操作者训练完成。训练完成后，可发出正式的语音指令，即可进入正式的语音识别模式。语音识别完成，通过指示灯模拟辨别是否正常发出指示信号
### 3.2 系统结构
整个语音控制系统以ARC EM处理器为核心，以语音识别为基础，通过语音指令完成对车内各项操作的控制。此控制系统主要由以下子系统构成：ARC EM核心处理器、稳压电源系统、触摸屏输入和显示系统、音频输入系统、信号采集和输出系统等。系统架构图如图3-1







