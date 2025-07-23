from flask import Flask, render_template, request, redirect, url_for, session
import requests
import json
from datetime import datetime
import os

app = Flask(__name__)
app.secret_key = 'your-secret-key-here'  # Change this to a random string

# Store businesses and incidents in memory (simple for MVP)
businesses = []
incidents = []

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/signup', methods=['POST'])
def signup():
    business = {
        'id': len(businesses) + 1,
        'name': request.form['business_name'],
        'industry': request.form['industry'],
        'size': request.form['size'],
        'email': request.form['email'],
        'signup_date': datetime.now()
    }
    businesses.append(business)
    
    # Store business ID in session for dashboard access
    session['business_id'] = business['id']
    
    return redirect(url_for('dashboard'))

@app.route('/dashboard')
def dashboard():
    # Get current business from session
    business_id = session.get('business_id')
    if not business_id:
        return redirect(url_for('home'))
    
    current_business = next((b for b in businesses if b['id'] == business_id), None)
    if not current_business:
        return redirect(url_for('home'))
    
    # Get CISA vulnerability data
    try:
        print("Fetching CISA data...")  # Debug line
        response = requests.get('https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json', timeout=10)
        data = response.json()
        vulns = data['vulnerabilities'][:5]  # Get top 5
        print(f"Found {len(vulns)} vulnerabilities")  # Debug line
    except Exception as e:
        print(f"Error fetching CISA data: {e}")  # Debug line
        # Fallback sample data
        vulns = [
            {
                'cveID': 'CVE-2024-SAMPLE',
                'vulnerabilityName': 'Sample Security Vulnerability',
                'shortDescription': 'This is sample vulnerability data. Real data will load from CISA when available.'
            }
        ]
    
    # Calculate personalized risk based on business profile
    risk_score = calculate_risk_score(current_business)
    
    # Get network statistics
    network_stats = {
        'total_businesses': len(businesses),
        'recent_incidents': len([i for i in incidents if (datetime.now() - i.get('timestamp', datetime.now())).days <= 7]),
        'your_risk_score': risk_score
    }
    
    return render_template('dashboard.html', 
                         business=current_business,
                         vulnerabilities=vulns,
                         **network_stats)

def calculate_risk_score(business):
    """Calculate a simple risk score based on business profile"""
    base_score = 3.0  # Default risk level
    
    # Industry risk multipliers
    industry_risk = {
        'financial': 4.5,
        'healthcare': 4.2,
        'retail': 3.8,
        'manufacturing': 3.5,
        'professional': 3.2,
        'other': 3.0
    }
    
    # Size risk multipliers (smaller = higher risk)
    size_risk = {
        'micro': 1.2,
        'small': 1.1,
        'medium': 1.0
    }
    
    industry = business.get('industry', 'other')
    size = business.get('size', 'small')
    
    risk_score = industry_risk.get(industry, 3.0) * size_risk.get(size, 1.0)
    return min(round(risk_score, 1), 5.0)

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 5000))
    app.run(host='0.0.0.0', port=port, debug=True)
