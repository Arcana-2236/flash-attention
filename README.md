# Global Token Support for sliding window in Flash-Attention

## FA kernel modification
1. Intra-tile level masking: Logical mask for GSW, but still have redundant computation --> 20% slow down
2. Inter-tile level skipping: Actual skip for GSW, faster, but currently still has some problem in mathmetic part --> ~4.4% slow down


## Run and modify the code
```
# Clone vllm
# Clone flash-attention
# Point vLLM to your local flash-attention and init submodules
export VLLM_FLASH_ATTN_SRC_DIR=/your-flash-attention-dir

# in flash-attention dir
git submodule update --init --recursive

# in vllm dir
# One time setup, rebuild vllm with flash-attention
python tools/generate_cmake_presets.py
uvx cmake --preset release

# Each time rebuild
uvx cmake --build --preset release --target install
```
