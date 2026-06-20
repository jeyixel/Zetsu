# **Zetsu AI \- Setup Guide**

Welcome to **Zetsu**\! This is a quick-and-dirty developer guide to getting this local RAG project running on your machine after cloning the repository.

## **Step 1: Set Up Python Virtual Environment**

Before downloading any dependencies, we need to isolate our Python environment so we don't mess up our global packages.

**1\. Create the virtual environment**

This command creates a folder named venv containing a local, isolated copy of Python.

python \-m venv venv

**2\. Activate the virtual environment**

This command tells your terminal to start using the isolated environment we just created. You'll know it's working when you see (venv) at the beginning of your command line.

* **On macOS/Linux:**  
  source venv/bin/activate

* **On Windows (Command Prompt):**  
  venv\\Scripts\\activate.bat

* **On Windows (PowerShell):**  
  venv\\Scripts\\Activate.ps1

## **Step 2: Install Python Dependencies**

Now that your virtual environment is active, you can install all the required Python libraries.

**Install requirements**

This reads our requirements.txt file and installs FastAPI, LangChain, BeautifulSoup, and all other required AI/web packages directly into your virtual environment.

pip install \-r requirements.txt

## **Step 3: Spin Up Docker Infrastructure**

*Note: You don't need to exit your Python virtual environment to run Docker commands. Docker runs globally on your machine, so it doesn't mind the venv being active\!*

**Start Ollama & ChromaDB**

This reads our docker-compose.yml file, downloads the official images for Ollama and ChromaDB, and boots them up in "detached" mode (-d) so they run quietly in the background.

docker-compose up \-d

## **Step 4: Download Zetsu's AI Models**

Our Ollama container is running, but it's empty. We need to download the AI models inside it.

**1\. Pull Llama 3.2 (The Brain)**

This jumps inside our running zetsu\_ollama container and downloads the llama3.2 model, which acts as the text generator for our assistant.

docker exec \-it zetsu\_ollama ollama pull llama3.2

**2\. Pull Nomic Embed Text (The Librarian)**

This tells our Ollama container to download nomic-embed-text, a small, super-efficient model that translates crawled text into coordinates (vectors) for ChromaDB to store.

docker exec \-it zetsu\_ollama ollama pull nomic-embed-text

## **Step 5: Environment Variables Setup**

Make sure to copy the template file to set up your environment configuration.

**Create your local environment file**

This copies the contents of .env.example into a brand-new .env file where we can customize settings.

cp .env.example .env

You are all set\! Let's get scraping and building\!