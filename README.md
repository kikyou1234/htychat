# htychat
使用llama-chinese微调技术用于无人值守客服系统

* 训练模型
链接：https://pan.baidu.com/s/1uLjNAXmOusXiIhNxK6u-tA 
提取码：1234 


* 预训练数据集准备


* 转化为数据格式

 ```
 {
    "instruction": "作为一名无人值守店铺的客服，你需要简单回答客户问题，回答字数限于30个字以内，客户的问题是 :",
    "input":  "问题",
    "output": "回答"
} 
 ```

* 模型训练 

使用4张3090进行全参数微调
```
export NCCL_P2P_DISABLE="1"
export NCCL_IB_DISABLE="1"
./run_sft.sh
```

* 模型合并
```
python merge_llama2_with_chinese_lora_low_mem.py  
       --base_model /root/model/chinese-alpaca-2-7b     
       --lora_model /root/test2/sft_lora_model     
       --output_type huggingface     --output_dir /root/model_output/llama-chinese-7b
```

* 模型推理加速

* 模型启动，使用API进行交互

```
python openai_api_server.py --base_model /root/model_output --gpus 0,1,2,3
```
