
# 





## 

- 

- 

- 

- 


- 

- 

- 

- 

- 

- 


- 

- 

- 

- 

- 

- 

- 

- 

- 

- 


## 

- 

- 

- 

- 

- 

- 

- 


## 

### 

```bash
git clone https://github.com/yourusername/ebook-to-audiobook-converter.git
cd ebook-to-audiobook-converter
```

### 

```bash
python3 -m venv venv
source venv/bin/activate  # For Windows, use `venv\Scripts\activate`
```

### 

```bash
pip install -r requirements.txt
```



### 



```python
import nltk
nltk.download('punkt')
```



```bash
python -m nltk.downloader punkt
```

### 



- 


```bash
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
```
- 






### 



- 


```bash
sudo apt-get install ffmpeg
```
- 




## 

- 


- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 


- 

- 

- 

- 

- 

- 

- 

- 

- 


- 

- 




```bash
pip install argparse nltk pydub ebooklib beautifulsoup4 tqdm gradio torch TTS torchaudio
```

## 

### 



```bash
python app.py
```



```
Running on local URL: http://localhost:7860
```



#### 

- 

- 

- 

- 


- 

- 

- 

- 

- 

- 

- 

- 

- 


### 



```bash
python app.py --headless --ebook path_to_ebook [options]
```

#### 

```bash
python app.py --headless --ebook mybook.epub --language en --temperature 0.7
```

## 





## 

### 

```bash
python app.py --headless --ebook mybook.epub --language en
```



### 

```bash
python app.py --headless --ebook mybook.epub --voice myvoice.wav --language en
```



### 

```bash
python app.py --headless --ebook mybook.epub --language en --use_custom_model True --custom_model_url "https://example.com/model.zip"
```



### 

```bash
python app.py --headless --ebook mybook.epub --language en --temperature 0.8 --speed 1.5 --top_k 40 --top_p 0.7
```



## 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 

- 


## 

### 





```
Error: Calibre's ebook-convert tool is not installed. Please install Calibre for this functionality.
```



- 

- 

- 


### 





```
LookupError:
**********************************************************************
  Resource punkt not found.
  Please use the NLTK Downloader to obtain the resource:
  >>> import nltk
  >>> nltk.download('punkt')
**********************************************************************
```



- 


```python
import nltk
nltk.download('punkt')
```
- 


```bash
python -m nltk.downloader punkt
```

### 





```
FileNotFoundError: [Errno 2] No such file or directory: 'ffmpeg'
```



- 

- 

- 


### 





```
FileNotFoundError: Custom model files not found.
```



- 

- 

- 


### 





```
RuntimeError: CUDA out of memory.
```



- 

- 

- 


### 





- 

- 

- 


### 





```
Audiobook created at ./Audiobooks/mybook.m4b
```





- 

- 

- 


### 





- 

- 


```python
device = torch.device("cpu")
```
- 


```bash
export CUDA_VISIBLE_DEVICES=""
```

## 

### 



### 



### 



- 

- 

- 


### 



### 



## 

- 

- 

- 

- 


## 



```
starting...
Device selected is: cuda
Running on local URL: http://localhost:7860
Running on local URL: http://localhost:7860
```



```
Downloading Model: 100%|██████████| 200M/200M [00:20<00:00, 10MB/s]
Extracting Files: 100%|██████████| 3/3 [00:01<00:00,  2.00file/s]
All required files (model.pth, config.json, vocab.json_) found.
Creating chapter-labeled book
Converted chapter 1 to audio.
Converted chapter 2 to audio.
Creating M4B from chapters
Combined audio saved to ./Audiobooks/mybook.m4b
Audiobook created at ./Audiobooks/mybook.m4b
```


