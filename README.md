# llama2-sft-chatbot

## License
This template is licensed to Customer subject to the terms of the license agreement between Domino and the Customer on file.

## About this project
In this project we demonstrate the use of a pre-trained Large Language Model (LLM) in Domino and the process of fine-tuning the model for a specific task. We will convert this model using `ctranslate2` to optimize its throughput and deploy it as a model API and app in Domino.

Fine-tuning a pre-trained LLM is a commonly used technique for solving NLP problems with machine learning. This is a typical transfer learning task where the final model is realised through a number of training phases:

1. The process typically begins with a pre-trained model, which is not task specific. This model is trained on a large corpora of unlabelled data 

2. The model undergoes a process of domain specific adaptive fine-tuning, which produces a new model with narrower focus or better alignment. This new model is better prepared to address domain-specific challenges as it is now closer to the expected distribution of the target data or responses the user expects. 

In this demo project we use the <> dataset , which provides <> samples of <>. This dataset is used in conjuction with <model>, which we fine-tune for the purpose of building a conversational assistant

The assets available in this project are:

* **llama2_guanaco.ipynb** - A notebook, illustrating the process of  fine tuning <> on the <> dataset
* **ct2_converter.ipynb** - A notebook that shows how to convert the fine tuned Huggingface model to an optimized `ctranslate2` model
* **model.py** - A scoring function, which is used to deploy the fine-tunned model as a [Domino API](https://docs.dominodatalab.com/en/latest/user_guide/8dbc91/host-models-as-rest-apis/)
* **app_streaming.py** - A Python file that embeds the `ctranslate2` model and allows for users to interact with the model as a Streamlit app
* **app.sh** - Launch instructions for the accompanying Streamlit app.

## Model API calls

The **model.py** provides a scoring function with the following signature: `generate(prompt)`. To test it, you could use the following JSON payload:

```
{
  "data": {
    "prompt": "What can I do in Paris for a day?"
  }
}
```

## Set up instructions

This project requires the following [compute environments](https://docs.dominodatalab.com/en/latest/user_guide/f51038/environments/) to be present. Please ensure the "Automatically make compatible with Domino" checkbox is selected while creating the environment.

**Environment Base** 

`quay.io/domino/pre-release-environments:domino-llm-environment.main.latest`

**Pluggable Workspace Tools** 
```
jupyterlab:
  title: "JupyterLab"
  iconUrl: "/assets/images/workspace-logos/jupyterlab.svg"
  start: [ "/opt/domino/workspaces/jupyterlab/start" ]
  httpProxy:
    internalPath: "/{{ownerUsername}}/{{projectName}}/{{sessionPathComponent}}/{{runId}}/{{#if pathToOpen}}tree/{{pathToOpen}}{{/if}}"
    port: 8888
    rewrite: false
    requireSubdomain: false
vscode:
 title: "vscode"
 iconUrl: "/assets/images/workspace-logos/vscode.svg"
 start: [ "/opt/domino/workspaces/vscode/start" ]
 httpProxy:
    port: 8888
    requireSubdomain: false
```

Please change the value in `start` according to your Domino version.


You also need to make sure that the hardware tier running the notebook or the fine-tuning script has sufficient resources. A GPU with >=16GB of VRAM is recommended. This project was tested on a V100 with 16GB VRAM


