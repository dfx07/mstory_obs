***

1/ Các tọa độ trong OpenGL cần chú tâm.

 - Clip
 - NDC : tọa độ tiêu chuẩn
 - View
 - Screen space : tọa độ pixel.

![[Pasted image 20250907100808.png]]

2/ Chuyển đổi tọa độ giữa các hệ tọa độ.

1.Clip to Screen.
 
Chúng ta cần độ phân giải của màn hình ở đây là view port.
```C++
vec2 clip_2_screen(vec4 vtx) 
{ 
	vec2 ndc = vtx.xy / vtx.w; 
	return (ndc * 0.5 + 0.5) * u_Viewport; 
}
```

2.Clip to NDC

``` C++
vec2 clip_2_ndc(vec4 clipPosition)
{
    return clipPosition.xy / clipPosition.w;
}
```

3.Pixel to Word


4.Word to Pixel.



3/ 


