# glslangValidator

Khronos 官方 glslang 的 `glslangValidator` 命令行工具，**静态链接 Linux x86-64 单文件**，零依赖，解压即用。

## 版本

- glslang: **14.3.0**
- GLSL: 4.60 / OpenGL ES GLSL: 3.20
- SPIR-V: 1.6 (via glslang)

## 用法

```
./glslangValidator <options> <shader-file>
```

### GLES 着色器校验（不生成 SPIR-V）

```
./glslangValidator -S frag --no-link fs.frag   # 片段着色器
./glslangValidator -S comp --no-link me.comp   # compute shader
```

### Vulkan 着色器校验（生成 SPIR-V）

```
./glslangValidator -V --target-env vulkan1.1 xxx.comp
./glslangValidator -V --target-env vulkan1.1 xxx.frag -o xxx.spv
```

### 常用选项

| 选项 | 说明 |
|---|---|
| `-S <stage>` | 指定着色器阶段：vert / frag / comp / geom / tesc / tese |
| `--no-link` | 单文件校验，不链接（适合独立片段/compute 源） |
| `-V` | 面向 Vulkan，输出 SPIR-V |
| `--target-env vulkan1.1` | 指定 Vulkan 目标版本（1.1 及以上） |
| `-o <file>` | SPIR-V 输出文件 |
| `-h` / `--help` | 帮助 |

## 环境要求

- Linux x86-64，任意发行版（glibc 版本无要求，已静态链接）
- 下载后 `chmod +x glslangValidator`（如无可执行权限）

## 构建信息

- 来源：https://github.com/KhronosGroup/glslang （tag 14.3.0）
- 构建：`cmake -DBUILD_SHARED_LIBS=OFF -DENABLE_OPT=OFF -DGLSLANG_TESTS=OFF` + `-static`
