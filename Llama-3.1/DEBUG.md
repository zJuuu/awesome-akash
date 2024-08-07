### Debugging VLLM Deployments

While deploying vLLM, you may encounter some issues. Here are some of the issues and how to resolve them:

**GPU:**

**H100:**

1. **Issue**: SDL, which works on `H100 80GB PCI`, did not work on `H100 80GB HBM3` and crashed with a `CUDA Out of Memory` error.

    **Additional Info**: HBM3 has a different memory architecture than PCI. Also, some providers run different NVIDIA drivers. These differences can cause issues with the memory requirements of the SDL.

    **Resolution**: Change the `--max-model-len` parameter to a lower value (i.e., 50% of the supported max context length) to fit the model in the memory.

    **Example**: `--max-model-len 131072` to `--max-model-len 65536` (50% of the supported max context lengt. You can find it for most models in the tokenizer.config.json file, i.e., [Meta-Llama-3.1-405B-Instruct-FP8 tokenizer_config.json](https://huggingface.co/meta-llama/Meta-Llama-3.1-405B-Instruct-FP8/blob/7c365a34d0fed5b4afb118cf253395f47f6efa72/tokenizer_config.json#L2060)).

2. **Issue**: SDL, which works on a different Provider has a different behavior and crashes with a unexpected error.

    **Additional Info**: Providers cache the Docker images. If the creator of the Docker image updates the image with the same tag, the provider may not pull the updated image. This can cause issues with the SDL.

    **Resolution**: Add the sha256 of the Docker image to the Docker image tag. This will force the provider to pull the updated image.

    **Example**: Suppose the Docker image tag is `huggingface/llama-3.1:latest`. Change it to `huggingface/llama-3.1:latest@sha256:1234567890abcdef`.

3. **Issue**: SDL, which works on a different Provider crashes with a `CUDA error: uncorrectable ECC error encountered` error.

    **Additional Info**: This error is due to the ECC memory error. ECC memory is a type of system memory that can detect and correct common kinds of internal data corruption. The ECC memory error can be caused by a hardware issue.

    **Resolution**: Try to run the SDL on a different provider or deploy it on the same provider on a different node.
    You can find the Node ID in the Events tab of console.akash.network. The output is similar to the following:
    ```[vllm]: [Normal] [Scheduled] [Pod] Successfully assigned 1vhjk6b5bs7p69nadik4n0kuru4bo17fisbn7lpqcs24g/vllm-0 to node4``` where `node4` is the Node ID.

    **Example**: /
