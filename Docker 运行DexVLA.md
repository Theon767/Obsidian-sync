数据在/sda/dataset 以及 /sda/models中
## 启动Docker
docker run -it --gpus all --shm-size=2g -e PYTHONPATH=/dexvla:/dexvla/policy_heads:$PYTHONPATH -v /sda/models:/mnt/data/models -v /sda/dataset:/mnt/data/datasets dexvla /bin/bash
## 训练
CUDA_VISIBLE_DEVICES=1 python train_vla.py \
--use_reasoning True \
--lora_enable True \
--action_dim 14 \
--state_dim 14 \
--flash_attn True \
--chunk_size 50 \
--load_pretrain_dit True \
--pretrain_dit_path /mnt/data/models/scale_dp_l/open_scale_dp_l_backbone.ckpt \
--policy_head_type scale_dp_policy \
--policy_head_size ScaleDP_L \
--image_size_stable "(320,240)" \
--image_size_wrist "(320,240)" \
--task_name example_tasks \
--model_name_or_path /mnt/data/models/Qwen2-VL-2B-Instruct \
--version v0 \
--tune_mm_mlp_adapter True \
--freeze_vision_tower True \
--freeze_backbone True \
--mm_use_im_start_end False \
--mm_use_im_patch_token False \
--image_aspect_ratio pad \
--bf16 True \
--output_dir /mnt/data/models/dexvla_qwen2_lora \
--max_steps 100000 \
--per_device_train_batch_size 1 \
--gradient_accumulation_steps 4 \
--save_strategy steps \
--save_steps 10000 \
--save_total_limit 50 \
--learning_rate 2e-5 \
--weight_decay 0. \
--warmup_ratio 0.01 \
--lr_scheduler_type constant \
--logging_steps 50 \
--tf32 True \
--model_max_length 2048 \
--gradient_checkpointing True \
--dataloader_num_workers 8 \
--lazy_preprocess True \
--policy_class scale_dp_policy \
--concat token_cat \
--report_to tensorboard \
--logging_dir /mnt/data/models/dexvla_train/log

## 推理
python evaluate/smart_eval_agilex.py