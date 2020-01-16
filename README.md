%% 12/1/2020; Renuka Soman
%% create a new image by using the neighbourhood pixel algorithm
clc; clear all; close all;
%%%%% neighbouring pixels algo
bin_dec=[];
I=imread('lena.jpg');     %original image
J=rgb2gray(I);       %grayscale of the image
[m1,n1]=size(J);     %get the rows and columns of image
x=max([m1,n1]);    %get the maximum value
res_img = imresize(J,[x x]);    %resizing the grayscale image
ori_arr=res_img;


[m,n]=size(ori_arr);

D = padarray(ori_arr,[1 1],0);
[rows cols]=size(D);

new_arr=zeros(m,n);

b=zeros(1,8);
for j=2:cols-1
    for i=2:cols-1
        i1=i-1; j1=j-1;
        a=D(i,j);
        b(5)=D(i-1,j-1); b(6)=D(i-1,j); b(7)=D(i-1,j+1); b(4)=D(i,j-1);   %getting the neighbourhood pixel values
        b(8)=D(i,j+1); b(3)=D(i+1,j-1); b(2)=D(i+1,j); b(1)=D(i+1,j+1);
        for k=1:8
            if b(k)>a
                bin_dec=[bin_dec 1];       %assigning the value 1 if greater than centre pixel else zero
            else
                bin_dec=[bin_dec 0];
            end
        end
        
%calculating the new decimal value for pixel
        dec_num=(128*bin_dec(1))+(64*bin_dec(2))+(32*bin_dec(3))+(16*bin_dec(4))+(8*bin_dec(5))+(4*bin_dec(6))+(2*bin_dec(7))+(1*bin_dec(8));
        new_arr(i1,j1)=dec_num;
        bin_dec=[];
    end
end
figure;
imshow(uint8(new_arr));

% figure;
% imshow(double(new_arr));
