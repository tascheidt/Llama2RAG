# Who, When, Why?
👨🏾‍💻 Original Author: Nick Renotte, updates from Todd as I bumbled through making it work for me <br />
📅 Version: 1.1 Sept 24, 2023<br />
📜 License: This project is licensed under the MIT license. Feel free to use it, just don't do bad things with it. </br>

# Environment notes 
1. Runpod using 1 A100-80GB GPU with 300GB of storage
2. Tried running across multiple GPUs using DataParallel to wrap the model but was not successful. I've left in the code to try to run in parallel but it would require more work to break up the workload into batches or find some other solution 
3. 300GB is required for the LLama 70B chat model. LLama2 requires ~140GB (70B x 2 bytes). The safetensors stored in the /model directory are another 140-150GB
4. If you want to access from an external port using streamlit later you also need to customize the deployment to expose TCP port 8501
3. Latest Pytorch environments are running Cuda11.8 so the notebook was modified accordingly 

# Jupyter notebook changes 
- would need to do a compare with Nick's original code to see all the changes but numerous small changes made to get code working
- Vectorstoreindex struggled with format of original vectors created by PyMuPDFReader so needed to ensure metadata was all changed to str data

# More granular steps to setup 
1. LLama2 download request - https://ai.meta.com/resources/models-and-libraries/llama-downloads/ . The turnaround on this is generally pretty quick and works well. You need to do this before you can run download.sh
2. The LLama models are gated models on huggingface so you must get access to the models before you can run the notebook. This can take multiple days so do it early. Here's the page for the 70B Chat model access - https://huggingface.co/meta-llama/Llama-2-70b-chat-hf . It seems like once you have access to one LLama model, you will have acess to all of the LLama2 models
3. Set up your Runpod environment - 1 A100 80GB GPU and 300GB of storage
4. Close the repository in the new Runpod environment
5. Run download.sh. Check first if the file has execute permissions using "ls -l download.sh". If there is not -x in the permissions then you need to run "chmod +x download.sh". Once the file has permissions run "./download.sh" from the terminal windown. You will be prompted for the URL in the email from Meta (this should work by simply cutting and pasting). You will also be prompted for the model you want to use. Download the 70B-chat model. This may take 20-30 minutes
6. Get your huggingface access token at https://huggingface.co/settings/tokens. This is immediate. Once you have it you need to add it to the appropriate place in the notebook
7. You should now be able to run the llama2 notebook and see the magic happen. Note that the first time this is run, you will need to wait for the sharded safetensors to download from huggingface. This could take 60 minutes so grab a drink and find something else to do for a while. It  can be run in parallel to the download of the LLama2 model.

And, boom! that should work

Note: I ran into out of memory errors repeatedly at the building model steps when the GPU would not release memory. The easiest fix was to restart the pod and then rerun the notebook. Not great but my other attempts at clearing the memory didn't work.  

# Streamlit version notes 
1. From the terminal prompt run: "pip install streamlit"
2. Next run "streamlit run app.py" from the terminal prompt
3. If you've configured your environment correctly that should work (but I never managed to get it to work) 

--------------- original readme from Nick ------------------------------

# Building LLama Banker
Doing RAG for Finance using LLama2. Highly recommend you run this in a GPU accelerated environment. I used a A100-80GB GPU on Runpod for the video!

## See it live and in action 📺
[![Tutorial](https://i.imgur.com/lqMC3K7.png)](https://youtu.be/SedGB8m2XLM 'Tutorial')

# Startup 🚀
1. Clone this repo `git clone https://github.com/nicknochnack/Llama2RAG`
2. Go into the directory `cd Llama2RAG`
3. Startup jupyter by running `jupyter lab` in a terminal or command prompt
4. Update the `auth_token` variable in the notebook. 
5. Hit `Ctrl + Enter` to run through the notebook! 
6. Go back to my YouTube channel and like and subscribe 😉...no seriously...please! lol 
7. If you want to start up the streamlit app run `streamlit run app.py` (make sure you update your auth token in there as well!)

# Other References 🔗
<p>-<a href="https://huggingface.co/meta-llama/Llama-2-70b-chat-hf">Llama 2 70b Chat Model Card</a>:hugging face model card on the model used for the video.</p>
<p>-<a href="https://www.llamaindex.ai/">Llama Index Doco</a>:sick library used for RAG.</p>

# Who, When, Why?
👨🏾‍💻 Author: Nick Renotte <br />
📅 Version: 1.x<br />
📜 License: This project is licensed under the MIT license. Feel free to use it, just don't do bad things with it. </br>

