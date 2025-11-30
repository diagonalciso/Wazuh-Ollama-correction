# Wazuh-Ollama-correction
Wazuh published a ollama integration in June 2025 but some stuff is now deprecated, so I corrected that part. 
https://wazuh.com/blog/leveraging-artificial-intelligence-for-threat-hunting-in-wazuh/

The main problem is langchain. The latest installation of langchain broke some stuff importing modules, so here is the correct code for installing pyhton3 and threathunter.py
I'm running Ubuntu 24.04

add the following to the installation procedure

sudo  apt install python3.12-venv
python3 -m venv ollama
source ollama/bin/activate

This bit hasn't changed

pip install paramiko python-daemon langchain langchain-community langchain-ollama langchain-huggingface faiss-cpu sentence-transformers transformers pytz hf_xet fastapi uvicorn 'uvicorn[standard]'

nano threat_hunter.py

# I changed some imports for langchain so it works with verion 1.1.0 Just replace everything from import json to import uvicorn. I will refine this once I have some time for it.

import json
import os
import gzip
from langchain_core.documents import Document
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_core.documents import Document
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_community.vectorstores import FAISS
from langchain_huggingface import HuggingFaceEmbeddings
from langchain_ollama import ChatOllama
from langchain_classic.chains import ConversationalRetrievalChain
from datetime import datetime, timedelta
from fastapi import FastAPI, WebSocket, WebSocketDisconnect
from fastapi.responses import HTMLResponse
from pydantic import BaseModel
from langchain_text_splitters import RecursiveCharacterTextSplitter
from langchain_community.vectorstores import FAISS
from langchain_huggingface import HuggingFaceEmbeddings
from langchain_ollama import ChatOllama
from langchain_core.documents import Document
from langchain_core.messages import SystemMessage, HumanMessage
import uvicorn




