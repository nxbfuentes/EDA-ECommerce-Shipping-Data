Option A: Using standard requirements.txt (Recommended for simplicity)
Create a file named requirements.txt in your project root directory and paste the following lines:

Plaintext
pandas
numpy
scikit-learn
matplotlib
seaborn
ipykernel
Open your terminal, navigate to your project folder, and create a virtual environment:

Bash
python -m venv zoomcamp-env
Activate the virtual environment:

Windows: zoomcamp-env\Scripts\activate

Mac/Linux: source zoomcamp-env/bin/activate

Install the packages from your file:

Bash
pip install --upgrade pip
pip install -r requirements.txt

, ensure your environment is activated in your terminal, then run this command to register it so Jupyter Notebook can see it:

Bash
python -m ipykernel install --user --name=zoomcamp-shipping --display-name "Python (Shipping Project)"