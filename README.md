# KBDecoder
Neural Networks for Text Correction and Completion in Keyboard Decoding

Code for the paper on  Neural Networks for Text Correction and Completion in Keyboard Decoding on 
Arxiv: https://arxiv.org/abs/1709.06429. The repository has the datasets the model is trained on, data loader, noise injection module, training module, realtime inference using a Flask based server and pretrained models. 


A. Datasets:
opensub-filtered-corrupted-ef.txt
train_twitter.txt


B. Vocabulary:
words.vocab


C. Instructions for training:

- Train with CNN attention:
python -u train_model.py --data_file=opensub-filtered-corrupted-ef.txt --is_training --batch_size=256 --use_attn=CNN

- Train with RNN attention:
python -u train_model.py --data_file=opensub-filtered-corrupted-ef.txt --is_training --batch_size=256 --use_attn=RNN 

- Train with LSTM (no attention):
python -u train_model.py --data_file=opensub-filtered-corrupted-ef.txt --is_training --batch_size=256 --lstm_cell


D. Instructions for Inference using the keyboard server from pretrained models:

1. Setup virtualenv
virtualenv tf
source tf/bin/activate

2. Install dependencies
pip install tensorflow-gpu
pip install flask

3. Extract attachment somewhere and run server (list the files first to see if you're in the correct directory)
python c2w_server.py --data_file=opensub-filtered-corrupted-ef.txt --checkpt_num=7500 --use_attn=RNN

4. Open browser and go to http://localhost:5000

E. Postprocessing for further correction through vocabulary:
python train_model.py --data_file=opensub-filtered-corrupted-ef.txt --checkpt_num=7500 --use_attn=RNN --retain_inputs --dictionary_correct

Here, retain-inputs do not actually correct, but pass the inputs straight through to the output based on the edit distance.

F. User study results:
userstudy-all

G. Pretrained models
enc-dec-chkpt-7500.data-00000-of-00001



