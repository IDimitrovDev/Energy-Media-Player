## Use DirectX Video Enhancements for Video Frames

Energy Media Player supports DirectX-based video enhancements for video frames when using either **FFmpeg DirectX hardware-accelerated decoding** or **FFmpeg software decoding**.

To enable hardware-accelerated DirectX decoding:

1. Open **Video settings**.
2. Set **Use hardware acceleration** to **On**.
3. Set **Hardware decoding mode** to **FFmpeg (DirectX 11)**.

![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/hardware_acceleration_selection.png)
When FFmpeg hardware acceleration is enabled, the player shows the GPU used for playback and video-frame decoding. On multi-GPU devices, such as laptops with both integrated and dedicated graphics cards, the GPU used by the player can be configured in Windows settings:

**System → Display → Graphics**

![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/decoding-gpu.png)

DirectX processing enables several video enhancements that can be applied to frames before they are displayed.

***

## 1. Upscaling

Upscaling is configured through the **Video upscaling method** setting. Available methods depend on GPU capabilities, so only supported options are shown.

![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/upscaling-method.png)

Supported upscaling methods include:

* **Bilinear**  
  Uses the Windows DirectX upscaler.

* **NVIDIA RTX Super Resolution**  
  Available only on NVIDIA RTX GPUs. This uses NVIDIA RTX Video Super Resolution. To use it, VSR must be enabled in the **RTX Video Enhancements** section of the NVIDIA app.

  ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/rtx%20enhancements.png)

* **Intel Video Super Resolution**  
  Available only on supported Intel devices.

* **Libplacebo (Lanczos or shader)**  
  Uses libplacebo upscaling. If a shader-based upscaler is active, that shader is used. Otherwise, libplacebo uses its default Lanczos upscaler.

After selecting an upscaling method, configure the **Upscaling mode**.

  ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/display-resolution.png)

In most cases, **Display resolution** or one of the fixed-resolution options is recommended. Hard resolution upscaling can be very GPU-intensive for large media files. For example, upscaling 4K video to 8K using a 2x scale can require significant GPU resources.

There is a hard resolution cap of **8K** for **Bilinear** and **Libplacebo**, and **5K** for **Intel Video Super Resolution** and **NVIDIA RTX Video Super Resolution**.

***

## 2. NVIDIA RTX HDR

On NVIDIA RTX GPUs, **RTX HDR** can be enabled to convert SDR media to HDR with strong visual results.

To use RTX HDR:

* RTX HDR must be enabled in the **RTX Video Enhancements** section of the NVIDIA app.
* Playback must run on an HDR-enabled display.
* The device must be plugged in.

 ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/rtx%20enhancements.png)
 
RTX HDR is available only for non-HDR media. If it is disabled, it can be enabled during playback using the **H** key, unless that key has been remapped. It can also be enabled from the **Video enhancements** context menu.

  ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/video-enhancements-menu.png)

***

## 3. Libplacebo / mpv-style Shader Enhancements

Libplacebo / mpv-style shaders, including `.glsl`, `.hk`, and `.hook` files, can be used to enhance video frames. They can provide effects such as:

* Upscaling, when libplacebo is selected as the upscaling method
* Adaptive sharpening
* Image modifications, such as:
  * Photo-negative colors
  * Black-and-white output
  * CRT-style video effects

Energy Media Player includes several default shaders and shader chains. These can be extended, modified, or removed.

  ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/shader-enhancements.png)

By default, shaders are stored in the player’s **LocalState** folder. This location can be changed using the **Select new shaders folder** button.

New shader files can also be added using **Import new shader file**.

All shader files found in the selected folder and in the installation location are listed under **Available Shader files**, where they can also be removed if needed.

To use one or more shader files, create a **shader chain**. A shader chain is an ordered list that defines the order in which shaders are applied. The order can affect the final result. For example, sharpening before upscaling is often more effective than sharpening after the frame has already been upscaled.

  ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/chain-editor.png)

To create a shader chain:

1. Select **Add Shader Chain**.
2. Use the shader chain editor to add a new chain.
3. Select the shaders to include.
4. Set a name for the shader chain.

After a shader chain is created, it is also added to the keyboard key bindings menu, where a custom shortcut can be assigned for faster activation.

  ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/keyboard-accelerators.png)

Shader chains can also be selected from the **Video enhancements** menu.

 ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/shader-chain-selector.png)

Shaders can be enabled or disabled by default using the **F1** key.
By default, libplacebo processing runs on the same GPU used for decoding. This can be changed using the **GPU adapter for libplacebo** setting.

 ![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/libplacebo-settings.png)

Libplacebo uses shader pipeline caches. If issues occur, these caches can be removed using the **Remove libplacebo caches** button. Normally, this is not required.

If troubleshooting is needed, logs can be collected by enabling logging. Logging may affect performance, especially when trace logging is enabled.

All video enhancements can be combined. For example, NVIDIA RTX Video Super Resolution can be used for upscaling, a Libplacebo shader chain can apply a photo-negative color effect, and RTX HDR can be enabled at the same time.

![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/video%20enhancements/combined-vsr-hdr-libplacebo.png)
***

## Software Decoding Enhancements

Video enhancements can also be enabled during software decoding. This is useful for media formats that do not support hardware decoding or when hardware acceleration is disabled.

To allow video enhancements during software decoding, enable:

*Allow D3D11-based post-processing enhancements—such as upscaling and RTX HDR when using software decoding*

This may affect performance because it requires CPU-to-GPU data transfers. With a sufficiently fast CPU and GPU, all video enhancements can be applied to software-decoded video frames.

***

## Multi-GPU Setup

On devices with multiple GPUs, such as laptops with both integrated and dedicated graphics cards, some video enhancements may not be available if the decoding GPU does not support them.

For example, video may be decoded on an Intel GPU while RTX VSR or RTX HDR requires an NVIDIA RTX GPU.

In these cases, enable:

*Allow offloading D3D11 post-processing enhancements, such as upscaling and RTX HDR, to a separate GPU. Requires a fast CPU for cross-GPU data transfer.*

This allows DirectX post-processing enhancements to be offloaded to a different GPU. Cross-GPU data transfer can be performance-intensive and requires a fast CPU.
