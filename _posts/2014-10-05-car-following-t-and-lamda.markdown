---
title: 两车跟驰模型中的T和Lamda
layout: post
guid: urn:uuid:2ef3550f-8cf3-400b-a55b-c512c9af8b2d
tags:
  - MATLAB
---

<!--
[![bridge to wonderland]({{ site.baseurl }}/media/files/2014/09/05/bridge-to-wonderland.jpg)](http://500px.com/photo/82158657)

[Lucian](http://lucianmarin.com/ "Lucian")
-->

下面的twobus函数作用是根据特定的T和lamda的值与两车跟驰模型计算得到两车的行驶轨迹x1和x2。

	function [y,z]=twobus(T,lamda)

	%初始化
	v1(100)=0;
	%v1(1)=40*3.6;
	v2(100)=0;
	%v2(1)=40*3.6;
	x1(100)=0;
	x1(1)=500;
	x2(100)=0;
	x2(1)=0;
	a1(100)=0;
	a2(100)=0;
	vmax=40*3.6;
	for k=1:101
		v1(k)=vmax*abs(sin(10*k*T));
	end
	 
	        for k=1:99        
	            a1(k)=(v1(k+1)-v1(k))/T;
	            x1(k+1)=x1(k)+v1(k)*T+1/2*a1(k)*(T)^2;
	            a2(k+1)=lamda*(v1(k)-v2(k));
	            v2(k+1)=v2(k)+a2(k)*T;
	            x2(k+1)=x2(k)+v2(k)*T+1/2*a2(k)*(T)^2;
	            
	            if x1(k)-x2(k)<0
	                break;
	            end
	        end
	        %数据存储
	    y=x1;
	    z=x2;
	    
	%     plot(y,z);
	end

datasave.m文件是调用上面的twobus函数计算100*100组不同的T和lamda组合所产生的x1和x2.并将数据储存到特定csv文件中。

	% name:datasave.m
	% author:Shuxiao Wang
	% time:2014.10.05
	% todo:将不同的T和lamda计算得到的x1和x2的值储存起来
	% 其中y是x1，z是x2，x1和x2各有100个。

	T=0.1:0.1:0.3;
	lamda=0.1:0.1:0.3;
	% a 作为写入csv文件的标记的头部
	% markInit 是写入csv文件的标记
	a='a';
	b='cw';


	for i=1:length(T)
	    for j=1:length(lamda)
	        [y,z] = twobus(T(i),lamda(j));
	        markInit1 = [a,num2str((i-1)*3*length(lamda)+3*j-2)];
	        markInit2 = [a,num2str((i-1)*3*length(lamda)+3*j-1)];
	        xlswrite('C:\MATLAB\20140926twobus\1.csv',y,'sheet1',markInit1);
	        xlswrite('C:\MATLAB\20140926twobus\1.csv',z,'sheet1',markInit2);
	        
	        markInitT = [b,num2str((i-1)*3*length(lamda)+3*j-2)];
	        markInitL = [b,num2str((i-1)*3*length(lamda)+3*j-1)];
	        xlswrite('C:\MATLAB\20140926twobus\1.csv',T(i),'sheet1',markInitT);
	        xlswrite('C:\MATLAB\20140926twobus\1.csv',lamda(j),'sheet1',markInitL);
	    end
	end


下面是一些用fprintf函数实现对txt文件的写入的方法。

	% 功能是一样的，用fprintf函数实现对txt文件的写入
	T=0.1:0.1:0.3;
	lamda=0.1:0.1:0.3;
	% a 作为写入csv文件的标记的头部
	% markInit 是写入csv文件的标记
	a='a';
	b='cw';

	fid = fopen('data.txt','a+');

	for i=1:length(T)
	    for j=1:length(lamda)
	        [y,z] = twobus(T(i),lamda(j));

	        fprintf(fid,'%g\t',y');
	        fprintf(fid,'%g\t',T(i));
	        fprintf(fid,'\n');
	        fprintf(fid,'%g\t',z');
	        fprintf(fid,'%g\t',lamda(j));
	        fprintf(fid,'\n\n');
	    end
	end

	fclose(fid);