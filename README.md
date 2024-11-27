# lec-2-PCM-Tramsmitter-and-Reciever
Code:
%DPCM Transmitter and Reciever
clc;
clear all;
close all;

fm=4; %input signal frequency
fs=20*fm; %sampling frequency
am=2; %input signal amplitude
t=0:1/fs:1;%time
x=am*cos(2*pi*fm*t);
figure(1);
plot(t,x,'r-');
hold on;
xlabel('Time');
ylabel('Amplitude');
%DPCM Transmitter
for n=1:length(x)
if n==1
e(n)=x(n);
eq(n)=round(e(n));
xq(n)=eq(n);
else
e(n)=x(n)-xq(n-1);
eq(n)=round(e(n));
xq(n)=eq(n)+xq(n-1);
end
end
%DPCM Reciever
for n=1:length(x)
if n==1
xqr(n)=eq(n);
else
xqr(n)=eq(n)+xqr(n-1);
end
end
figure(1);
plot(t,xqr,'k-');
xlabel('Time');
ylabel('Amplitude');
legend('Original signal','Reconstructed signsl');
%Low pass filter
[num, den]=butter(2,4*fm/fs);
roc_op=filter(num,den,xqr);
figure(2);
plot(t,roc_op,'k-');
xlabel('Time');
ylabel('Amplitude');
title('Smoothed signal')
Title: Line Coding
Code:
n=[1,0,1,0,1];%Number of binary data input
for b=1:length(n)
if n(b)==1
a(b)=3;
else
a(b)=0;
end
end
i=1;%index value starts from 1 in MATLAB. So variable 1 is used to index thw input(n)
t=0:0.01:length(n)%TIme axis begin from 0 to length of n
for j=1:length(t)
if t(j)<=i
y(j)=a(i);
else
y(j)=a(i);
i=i+1;
end
end
plot(t,y,'r');

Title: RZ Unipolar
Code:
n=[1,0,1,0];
i=1;
a=0;
b=0.5;
t=0:0.01:length(n);
y=zeros(size(t));
for j=1:length(t)
if t(j)>=a && t(j)<=b
y(j)=n(i);
elseif t(j)>b && t(j)<=i
y(j)=0;
else
i=i+1;
a=a+1;
b=b+1;
end
end
plot(t,y)

Title: RZ Polar
Code:
n=rand(1,10);
i=1;
a=0;
b=0.5;
t=0:0.01:length(n);
y=zeros(size(t));
for j=1:length(t)
if t(j)>=a && t(j)<=b
if i<=length(n)
y(j)=n(i);
else
y(j)=0;
end
elseif t(j)>b && t(j)<=i
y(j)=0;
else
i=i+1;
a=a+1;
b=b+1;
end
end
plot(t,y);
axis([0 length(n) -2 2 ]);
xlabel('Time');
ylabel('Value');
title('Plot of y against t');
