
## About this project

This project demonstrates how (small) language models can be finetuned using techniques such as 
- Full Finetuning
- LORA
- QLORA
- Prefix Finetuning

It also analyzes the impact of increasing training data size as well as impact of increasing training parameters on evaluation metrics

The task being undertaken here is Text to SQL generation

### Running Notebooks
1. **Instantiating virtual environment**:
Virtual env contains the dependent libraries that are required to run the project. As it can be pretty large in size, it has not been packaged with the project and should be instantiated before the notebooks are run. 

    The notebooks have been developed using Python 3.11 so it is recommended to have same or compatible version 

To create the virtual env run: 
```python
python3.11 -m venv venv
```
To activate the virtual env run: 
```python
source venv/bin/activate
```

**Running the notebooks**:

The notebooks can be run by clicking on Run All option
They follow following overall structure:
- Install required libraries
- Import dependencies
- Intialize pretrained model
- Define functions for calculating evaluation metrics
- Initialize pretuning configurations
- Preprocess inputs and set training arguments
- Perform finetuning and save the finetuned model configs
- Load finetuned model configs, apply to base model and evaluate test dataset
- Provide a function to take any random input as an argument and generate its SQL

**NOTE**: 

 - Finetuning has been commented out. To finetune the model make sure to uncomment it
 - Device type has been set as per Mac's Silicon chip. If you are training on CUDA device, please update device setting accordingly
 - If you only need to peform inferencing, it has been tested to run on CPU as well (although it may be slower than running on a GPU)

**About the notebooks**:

  `FlanT5Large_SQL_Pretrained.ipynb` - This notebook performs benchmarking on pretrained Flan T5 Large model. Pretrained model has been found to peform poorly on Text 2 SQL Generation task

  `finetuning_FlanT5Large_SQL_LORA.ipynb` - This notebook performs finetunes Flan T5 Large model using LORA technique on training size of 20000 records. LORA technique turned out to be the best of all finetuning techniques for Text 2 SQL Generation task

   `finetuning_FlanT5Large_SQL_QLORA.ipynb` - This notebook performs finetunes Flan T5 Large model using QLORA technique on training size of 20000 records. QLORA technique peformed poorly for Text 2 SQL Generation task

  `finetuning_FlanT5Large_SQL_PrefixTuning.ipynb` - This notebook performs finetunes Flan T5 Large model using Perfix tuning technique on training size of 20000 records. Prefix finetuning technique peformed poorly for Text 2 SQL Generation task

   `finetuning_FlanT5Large_SQL_FullFT.ipynb` - This notebook performs full finetuning on Flan T5 Large model on training size of 1000 records only. Any higher number of training size was resulting in OOM error on the setup being used. With fulltuning on such a small dataset, the model peformed poorly for Text 2 SQl Generation task
   
   **NOTE**: Full tuning configs for the model have not been bundled due to size limitations. Please train the model first before running evaluation. 

   `finetuning_FlanT5Large_SQL_LORA_largeDS.ipynb` - This notebook performs finetunes Flan T5 Large model using LORA technique on an increased training size of 60000 records. However increasing training size by 3 times yielded only slight improvement in evaluation scores

   `finetuning_FlanT5Large_SQL_LORA_moreParams.ipynb` - This notebook performs finetunes Flan T5 Large model using LORA technique on an increased trainable params (1.19% from 0.3% earlier). However increasing trainable params yielded only slight improvement in evaluation scores




## 📊 Results Summary

### Performance Comparison
| Technique | BLEU | ROUGE-L | METEOR | GLEU | Trainable Params |
|-----------|------|---------|--------|------------|------------------|
| Pre-trained | 0.02 | 0.18 | 0.14 | 0.27 | 0% |
| LoRA | 0.47 | 0.66 | 0.66 | 0.7 | 0.3% |
| QLoRA | 0.0 | 0.03 | 0.20 | 0.18 | 0.3% |
| Prefix Tuning | 0.01 | 0.18 | 0.12 | 0.23 | 0.12% |
| Full Fine-tuning | 0.11 | 0.37 | 0.32 | 0.48 | 100% |

### Key Findings
- **LoRA** provides the best performance-to-efficiency ratio

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines
- Add comprehensive documentation for new techniques
- Include evaluation metrics for all experiments
- Provide reproducible results with seed settings
- Test on multiple hardware configurations

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## �� Acknowledgments

- **Hugging Face** for the transformers and PEFT libraries
- **GretelAI** for the synthetic Text-to-SQL dataset
- **Apple** for MPS backend support
- **Microsoft** for the LoRA technique

---

**Note**: This project is designed for educational and research purposes. Results may vary based on hardware configuration and dataset variations.