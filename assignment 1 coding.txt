clc;
clear;
close all;

image = imread ('C:\nomborPlet.png');
image = im2bw(image);

image(117,417,1)=0;
image(112,418,1)=0;

cc = bwconncomp(image,4);
L1 = labelmatrix(cc);
C1 = labelmatrix(cc);
RGB = label2rgb(C1);

% 8-connectivity
image(77,151,1)=0;
image(112,312,1)=0;
image(117,416,1)=0;
image(112,417,1)=0;
image(111,417,1)=0;
image(116,416,1)=0;

cc2 = bwconncomp(image);
L2 = labelmatrix(cc2);
C2 = labelmatrix(cc2);

s = regionprops(L1,'Centroid');
s2 = regionprops(L2,'Centroid');

subplot(1,2,1);
imshow(label2rgb(L1),'InitialMagnification','fit');
title('4-connectivity');
hold on

for k = 1:numel(s)
    c = s(k).Centroid;
    text(c(1),c(2),sprintf('%d',k),'HorizontalAlignment','center','VerticalAlignment','middle');
end

subplot(1,2,2);
imshow(label2rgb(L2),'InitialMagnification','fit');
title('8-connectivity');


for k = 1:numel(s2)
    c = s2(k).Centroid;
    text(c(1),c(2),sprintf('%d',k),'HorizontalAlignment','center','VerticalAlignment','middle');
end
hold off

