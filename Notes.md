# notes


python fastchat/serve/cli.py --model-path LLMs/lmsys/vicuna-7b-v1.5-16k --style simple
python fastchat/serve/cli.py --model-path LLMs/lmsys/vicuna-7b-v1.5-16k --style rich
python fastchat/serve/cli.py --model-path LLMs/lmsys/vicuna-7b-v1.5-16k --style programmatic


python fastchat/serve/cli.py --model-path LLMs/lmsys/vicuna-7b-v1.5-16k --num-gpus 2


fine-tuning
```bash
torchrun --nproc_per_node=4 --master_port=20001 fastchat/train/train_mem.py \
    --model_name_or_path ~/model_weights/llama-7b  \
    --data_path data/dummy_conversation.json \
    --bf16 True \
    --output_dir output_01 \
    --num_train_epochs 3 \
    --per_device_train_batch_size 2 \
    --per_device_eval_batch_size 2 \
    --gradient_accumulation_steps 16 \
    --evaluation_strategy "no" \
    --save_strategy "steps" \
    --save_steps 1200 \
    --save_total_limit 10 \
    --learning_rate 2e-5 \
    --weight_decay 0. \
    --warmup_ratio 0.03 \
    --lr_scheduler_type "cosine" \
    --logging_steps 1 \
    --fsdp "full_shard auto_wrap" \
    --fsdp_transformer_layer_cls_to_wrap 'LlamaDecoderLayer' \
    --tf32 True \
    --model_max_length 2048 \
    --gradient_checkpointing True \
    --lazy_preprocess True
```

