---
title: 对NGSIM数据协方差处理草稿
layout: post
guid: urn:uuid:2ef3550f-8cf3-400b-a55b-c512c9af8b2d
tags:
  - MATLAB
---

这是系统辨识课上给的对NGSIM数据处理的一小部分，这部分的主要作用是对三个.mat文件中的一个进行处理，计算得到前后车速度和加速度的协方差。应该还有bug，我尝试了一下计算前1000行数据，发现无法得到正确的结果，思路仅供参考，debugging...

	clc;
	clear;
	load ('outdata_0500_0515.mat');% 加载需要处理的数据

	%------------------DEFINE Begin-------------------------
	nowCarLineNo=1;%本车开始时的行号
	nowCarLineNum=0;%本车数据总行数

	nowCarNum=0;% 本车车号
	nowCarV=zeros(1,1000);% 本车速度
	nowCarA=zeros(1,1000);% 本车加速度

	froCarLineNo=1;%前车开始时的行号
	froCarLineNum=0;%前车数据总行数

	froCarNum=0;% 前车车号
	froCarV=zeros(1,1000);% 前车速度
	froCarA=zeros(1,1000);% 前车加速度

	row=size(outdata);
	%rowNum=row(1,1);
	%------------------DEFINE End---------------------------

	%------------------Detect Begin-------------------------
	rowNum=1000;
	i=1;
	while (i<rowNum)
	    nowCarLineNo=i;
	    nowCarNum=outdata(i,1);
	    froCarNum=outdata(i,7);
	    if (froCarNum~=0)
	        while (outdata(i,1)==nowCarNum)
	            froCarLineNo=i;
	            nowCarLineNum=+1;
	%             froCarLineNum=+1;
	            nowCarV(i-nowCarLineNo+1)=outdata(i,4);
	            nowCarA(i-nowCarLineNo+1)=outdata(i,5);
	            froCarV(i-nowCarLineNo+1)=outdata(i,10);
	            froCarA(i-nowCarLineNo+1)=outdata(i,11);
	            i=+1;
	        end
	        froCarLineNum=sum(froCarV>0);
	        %todo:计算前后车速度和加速度协方差
	        covCarV=cov(nowCarV(1,1:froCarLineNum),froCarV(1,1:froCarLineNum));
	        covCarA=cov(nowCarA(1,1:froCarLineNum),froCarA(1,1:froCarLineNum));
	    else
	        while (outdata(i,1)==nowCarNum)
	            i=+1;
	        end
	    end
	end
	%------------------Detect end---------------------------