import json
import os
import requests 
import jwt      
from flask import Flask, request, jsonify
from groq import Groq
from solana.rpc.api import Client
from solders.pubkey import Pubkey
import ows  
from flask_cors import CORS 

app = Flask(__name__)
CORS(app) 

# --- CONFIG & ENVIRONMENT ---
G_KEY = os.getenv("GROQ_API_KEY")
EXCHANGE_KEY = os.getenv("EXCHANGE_RATE_API_KEY") 
SOLANA_RPC = "https://api.devnet.solana.com" 

client = Groq(api_key=G_KEY)
solana_client = Client(SOLANA_RPC)

# --- ZENTI TREASURY SETUP ---
# Default Demo User
DEMO_USER = {
    "email": "senseii@example.com",
    "address": "FMm5Zf3jdr2EmEPkNpD96wRnPYNSX8NGEn2tagxPf9Fm" 
}

# The main Treasury address checked by USSD
VAULT_ADDR = os.getenv("VAULT_ADDRESS", DEMO_USER["address"])

def get_live_ngn_rate():
    try:
        url = f"https://v6.exchangerate-api.com/v6/{EXCHANGE_KEY}/pair/USD/NGN"
        response = requests.get(url).json()
        return response.get('conversion_rate', 1550.0)
    except:
        return 1550.0 # Fallback 

def parse_zenti_ai(text):
    prompt = f"Zenti AI Parser: '{text}'. Return ONLY JSON: {{\"amount_sol\": float, \"recipient\": \"string\"}}"
    chat = client.chat.completions.create(
        model="llama-3.3-70b-versatile",
        messages=[{"role": "user", "content": prompt}],
        response_format={"type": "json_object"}
    )
    return json.loads(chat.choices.message.content)

# --- USSD CORE ---

@app.route("/ussd", methods=['GET', 'POST'])
def ussd():
    # Africa's Talking sends data via POST/GET
    user_text = request.values.get("text", "")
    
    if user_text == "":
        return "CON Welcome to Zenti Treasury\n1. My Balance (₦)\n2. Pay Supplier"
    
    elif user_text == "1":
        # Get Real Solana Balance
        pubkey = Pubkey.from_string(VAULT_ADDR)
        balance_resp = solana_client.get_balance(pubkey)
        sol_bal = balance_resp.value / 10**9
        
        rate = get_live_ngn_rate()
        # Mock Sol Price for Demo ($150)
        naira_bal = sol_bal * 150 * rate 
        return f"END Zenti Balance\n₦{naira_bal:,.2f}\n({sol_bal:.4f} SOL)"
    
    elif user_text == "2":
        return "CON Enter Payment:\n(Example: '0.1 to address')"
    
    elif user_text.startswith("2*"):
        raw = user_text.split("*")[-1]
        data = parse_zenti_ai(raw)
        tx_hash = "5vBv...Zenti_Demo" # Placeholder for live signing
        return f"END Zenti Payment Sent!\n{data.get('amount_sol')} SOL to {data.get('recipient')[:6]}...\nTX: {tx_hash}"

    return "END Error: Invalid input"

@app.route("/status", methods=['GET'])
def status():
    return {"status": "Zenti Engine Online", "network": "Solana Devnet"}

if __name__ == "__main__":
    port = int(os.environ.get("PORT", 8080))
    app.run(host='0.0.0.0', port=port)

