# Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

# Aim:
To write and implement Python code that integrates with multiple AI tools 
(such as OpenAI GPT, Hugging Face, and Google Gemini) to automate API interactions, 
compare outputs, and generate actionable insights.
# AI Tools Required:
  OpenAI GPT-3.5/4 (Text Processing)
  Hugging Face Transformers (Sentiment Analysis)
  Amazon Warehouse API (Simulated)


## **Algorithm & Implementation**

### **1. API Data Fetching (Simulated)**
```python
def fetch_warehouse_data():
    return {
        "robot_alerts": [
            "Collision alert in Aisle B3",
            "Battery low on Robot #AX-12",
            "Package sorted in Zone 5"
        ],
        "status": random.choice(["Operational", "Maintenance_Needed"])
    }
```

### **2. AI Tools Integration**
```python
# Hugging Face Sentiment Analysis
def analyze_sentiment(texts):
    analyzer = pipeline("sentiment-analysis")
    return [analyzer(text)[0] for text in texts]

# OpenAI Summarization
def generate_summary(text, api_key):
    openai.api_key = api_key
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role":"user", "content":f"Summarize these alerts: {text}"}]
    )
    return response.choices[0].message['content']
```

### **3. Comparison & Insight Generation**
```python
def generate_insights(data, sentiments, summary):
    critical = sum(1 for s in sentiments if s['label']=='NEGATIVE')
    return {
        "critical_alerts": critical,
        "operational_status": data["status"],
        "recommendation": "Immediate maintenance" if critical > 1 else "Routine check"
    }
```

### **4. Complete Workflow**
```python
def main():
    # 1. Fetch Data
    data = fetch_warehouse_data()
    
    # 2. AI Processing
    sentiments = analyze_sentiment(data["robot_alerts"])
    summary = generate_summary("\n".join(data["robot_alerts"]), "your_openai_key")
    
    # 3. Generate Insights
    insights = generate_insights(data, sentiments, summary)
    
    # 4. Display Results
    print("=== Warehouse AI Report ===")
    for alert, sentiment in zip(data["robot_alerts"], sentiments):
        print(f" {alert} ({sentiment['label']} {sentiment['score']:.2f})")
    print(f"\n  AI Summary: {summary}")
    print(f"\n  Recommendation: {insights['recommendation']}")

if __name__ == "__main__":
    main()
```

---

## **Execution Steps:**  
1. Install dependencies:
   ```bash
   pip install transformers openai
   ```
2. Set OpenAI API key  
3. Run script:
   ```bash
   python warehouse_ai.py
   ```

---

## **Input Prompt:**

"Write a Python program that fetches simulated warehouse robot alert data, uses Hugging Face Transformers to analyze sentiment for each alert, and uses OpenAI GPT (via API) to summarize the alerts. Based on sentiment and operational status, generate maintenance recommendations. The output should display individual alerts with sentiment scores, a summary of events, and a final recommendation. Use a modular structure with clearly defined functions for data fetching, sentiment analysis, OpenAI summarization, and insight generation."

## **Output:**
```
=== Warehouse AI Report ===
Collision alert in Aisle B3 (NEGATIVE 0.97)
Battery low on Robot #AX-12 (NEGATIVE 0.89)
Package sorted in Zone 5 (POSITIVE 0.95)

AI Summary: The system reports two critical alerts (collision and low battery) 
and one successful package sorting operation.

Recommendation: Immediate maintenance
```

---

## **Conclusion:**  
The system successfully demonstrates:  

1. **Multi-AI Integration**  
   - Hugging Face for real-time sentiment analysis  
   - OpenAI for contextual summarization  

2. **Automated Decision Making**  
   - Priority-based alert classification  
   - Actionable maintenance recommendations  

3. **Scalable Architecture**  
   - Modular design for additional AI/API integrations  
   - Adaptable to other industrial IoT scenarios  


# Result: The corresponding Prompt is executed successfully.
