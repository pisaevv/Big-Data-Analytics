# Market Sentiment Analysis - Nvidia RTX 40 Series GPUs

A comprehensive big data analytics project analyzing market sentiment and 
consumer perception of Nvidia RTX 40 series graphical processing units.

---

## 👨‍💻 Developer

Bislan Pisaev, Akmaljon Negmatulloev

---

## 📋 Project Overview

In late October 2023, NVIDIA released the RTX 40 series lineup of graphics 
cards, which received significant backlash from the gaming community. 
While higher-end cards represented breakthroughs in performance, 
budget-oriented models failed to capture their target markets effectively. 
This research analyzes consumer sentiment to understand what went wrong 
with the RTX 40 series and provide insights for future product releases.

---

## 🎯 Problem Definition

To comprehensively understand consumer sentiment towards the RTX 40 Series 
graphics cards and identify their shortcomings compared to competitors in 
the market.

---

## 📊 Table of Contents & Methodology

### 1. Introduction and Problem Definition

**Research Context:**
The RTX 40 series graphics cards presented a paradox in the market. 
Despite technical improvements over previous generations and superior 
architecture, budget and mid-range cards underperformed in market 
reception. Even though each card performed better than its predecessor, 
none became top recommendations in their respective price categories.

**Key Issues Identified:**
- Budget cards (RTX 4060) criticized for insufficient VRAM
- Poor value proposition compared to previous generation
- Pricing misalignment with performance improvements
- Limited appeal to target gaming demographic

**Research Objective:**
Analyze social media sentiment to identify specific pain points and 
consumer expectations, providing actionable insights for future GPU 
releases (RTX 50 series).

---

### 2. Data Collection

**Data Source:** Twitter/X platform

**Collection Methodology:**
- Automated web scraping using Selenium WebDriver
- Keyword-based filtering system
- Time-bound data collection during post-launch period

**Keyword Categories:**

**NVIDIA Keywords (40 keywords):**
- Product-specific: RTX 4060, RTX 4070, RTX 4080, RTX 4090
- Technology: DLSS 3, Frame Generation, Ray Tracing
- Performance metrics and specifications

**Comparison Keywords (20 keywords):**
- vs, comparison, better, worse
- Value, price-to-performance
- Worth it, upgrade, purchase decision

**Competitor Keywords (15 keywords):**
- AMD Radeon RX 7000 series
- Intel Arc graphics
- Previous gen alternatives

**Data Volume:**
- **Nvidia-related posts:** ~5,000 tweets
- **Competitor-related posts:** ~4,000 tweets
- **Total dataset:** 9,000+ social media posts

---

### 3. Data Preprocessing

**Technologies Used:**
- Python 3.8+
- Pandas & NumPy for data manipulation
- NLTK for natural language processing
- BERT Tokenizer (Transformers library)
- PyTorch for model preparation
- Scikit-learn for data splitting

**Preprocessing Pipeline:**

**Step 1: Data Loading**
```python
nvidia_frame = pd.read_csv("nvidia_data.csv")
competitors_frame = pd.read_csv("competitors_data.csv")
```

**Step 2: Data Cleaning**

*Duplicate Removal:*
- Removed duplicate posts based on content
- Ensured unique entries for accurate sentiment analysis

*Text Cleaning Operations:*
- Emoji removal and unicode normalization
- URL and mention stripping
- Hashtag cleaning and separation
- Special character removal
- Punctuation normalization
- Multiple whitespace reduction

**Step 3: Data Transformation**
- Datetime conversion for temporal analysis
- Calculation of post recency (days since posting)
- Feature engineering for engagement metrics

**Step 4: Data Preparation**
- Train/Validation split: 80/20 ratio
- Stratified sampling to maintain sentiment distribution
- Random state: 42 for reproducibility

**Step 5: Tokenization**
- BERT base model (uncased) tokenization
- Maximum sequence length: 64 tokens
- Padding and truncation for uniform input size
- Attention mask generation

**Step 6: DataLoader Configuration**
- Batch size: 4 for optimal memory usage
- Random sampling for training data
- Sequential sampling for validation data
- TensorDataset creation for PyTorch compatibility

---

### 4. Data Analysis

**Analysis Framework:** SQL-based sentiment aggregation with weighted 
metrics

**Question 1: General Sentiment Distribution**

*Methodology:*
- Sentiment classification: 0 (negative), 1 (neutral), 2 (positive)
- Weighted scoring based on:
  - Likes per view ratio
  - Shares (comments + reposts)
  - Total engagement metrics

*Results:*

| Metric | Competitors | NVIDIA RTX 40 |
|--------|-------------|---------------|
| Negative Total | 82,140 | 142,338 |
| Neutral Total | 127,239 | 1,124,049 |
| Positive Total | 229,482 | 1,702,794 |
| Negative Avg | 33.79 | 36.87 |
| Neutral Avg | 52.34 | 291.13 |
| Positive Avg | 94.40 | 441.02 |

*Key Finding:* NVIDIA received significantly higher positive sentiment 
overall, but also attracted more negative attention, indicating polarized 
consumer opinions.

---

**Question 2: Geographic Distribution**

*Methodology:*
- Currency mention detection (Naira, KES, EUR, USD, etc.)
- Regional keyword identification
- Geographic sentiment mapping

*Results:*

| Region/Country | Competitors | NVIDIA |
|----------------|-------------|--------|
| Nigeria | 24 | 461 |
| Kenya | 58 | 78 |
| Europe | 34 | 23 |
| USA | 9 | 23 |
| UK (GBP) | 15 | 15 |
| Switzerland | 4 | 8 |
| Ghana | 40 | 7 |
| India | 2 | 2 |
| China | 0 | 2 |
| Japan | 0 | 1 |

*Key Finding:* African markets (Nigeria, Kenya) showed exceptionally high 
engagement, likely due to pricing concerns and import challenges. Emerging 
markets demonstrated greater sensitivity to GPU pricing.

---

**Question 3: Keyword Association Analysis**

*Positive Keywords:*

| Keyword | Competitors | NVIDIA |
|---------|-------------|--------|
| high | 175 | 255 |
| cool | 81 | 144 |
| good | 61 | 69 |
| great | 54 | 47 |
| efficient | 17 | 45 |
| amaze | 23 | 33 |
| beauty | 18 | 31 |
| impress | 25 | 31 |
| smooth | 8 | 24 |
| solid | 11 | 21 |

*Negative Keywords:*

| Keyword | Competitors | NVIDIA |
|---------|-------------|--------|
| low | 182 | 318 |
| limited | 54 | 47 |
| bad | 10 | 20 |
| disappointing | 2 | 5 |
| overheating | 1 | 3 |
| poor | 3 | 3 |
| struggling | 2 | 2 |
| terrible | 3 | 1 |
| underwhelming | 1 | 1 |

*Key Finding:* The word "low" appeared 318 times in NVIDIA discussions, 
primarily referring to VRAM capacity concerns. "Limited" was frequently 
associated with feature restrictions on budget models.

---

### 5. Conclusion

**Key Findings:**

**1. Polarized Market Reception**
The analysis revealed a **dichotomy in consumer sentiment**. While Nvidia 
RTX 40 series achieved high positive sentiment scores (441.02 average), 
negative sentiment was also elevated (36.87) compared to competitors. This 
polarization indicates that while enthusiasts and high-end users praised 
the technology, mainstream consumers felt underserved.

**2. Geographic Market Insights**
- **Emerging markets dominated discussions:** Nigeria led with 461 
mentions, indicating high price sensitivity in developing economies
- **African markets highly engaged:** Kenya, Ghana, and Nigeria 
collectively represented the majority of regional discussions
- **Western markets relatively quiet:** USA and Europe showed lower 
engagement, suggesting different purchasing patterns

**3. Primary Pain Points**

**VRAM Limitations:**
- RTX 4060 8GB VRAM heavily criticized
- "Low" mentioned 318 times, primarily regarding memory capacity
- Budget cards perceived as artificially limited

**Value Proposition Issues:**
- Performance improvements didn't justify price premiums
- Previous generation alternatives offered better value
- Mid-range segment particularly problematic

**Feature Segmentation:**
- Budget cards lacked features present in higher tiers
- Artificial product differentiation frustrated consumers
- Limited upgrade path from previous generation

**4. Successful Elements**
- High-end cards (4090, 4080) praised for performance
- DLSS 3 and Frame Generation technology well-received
- Power efficiency improvements acknowledged
- Ray tracing performance improvements noted

---

**Limitations of This Study:**

1. **Data Source Constraints:** Analysis limited to Twitter/X platform; 
may not represent entire consumer base or purchasing patterns
2. **Temporal Scope:** Data captured during launch period; long-term 
sentiment evolution not included
3. **Language Barriers:** Primarily English-language posts; non-English 
markets underrepresented
4. **Sentiment Classification:** Automated sentiment may miss sarcasm, 
nuance, or context-specific meanings
5. **Selection Bias:** Social media users may not represent typical 
consumers
6. **Regional Sampling:** Geographic analysis based on currency mentions 
may have accuracy limitations

---

**Recommendations for RTX 50 Series Launch:**

1. **VRAM Configuration:**
   - Increase VRAM on budget cards (minimum 12GB for x60 tier)
   - Eliminate artificial memory limitations
   - Match or exceed competitor offerings

2. **Value Engineering:**
   - Ensure performance-to-price ratio meets market expectations
   - Competitive pricing in mid-range segment ($300-$500)
   - Clear upgrade path from RTX 30 series

3. **Feature Democratization:**
   - Make DLSS 3 available across entire product stack
   - Reduce artificial feature segmentation
   - Include all technologies in budget models

4. **Regional Pricing Strategy:**
   - Address emerging market pricing concerns
   - Consider regional economic factors
   - Improve availability in high-engagement markets (Africa, Southeast 
Asia)

5. **Market Communication:**
   - Transparent specification communication
   - Clear performance metrics and comparisons
   - Honest positioning against previous generations

6. **Product Segmentation:**
   - Avoid cannibalization between tiers
   - Ensure each SKU has compelling unique value
   - Better differentiation without artificial limitations

---

**Future Research Directions:**

- **Longitudinal Analysis:** Track sentiment evolution 6-12 months 
post-launch
- **Competitor Deep Dive:** Direct AMD Radeon RX 7000 vs RTX 40 series 
comparison
- **Purchase Correlation:** Link sentiment to actual sales data
- **Professional vs Gaming:** Separate analysis for different user 
segments
- **Price Elasticity:** Quantify price sensitivity across market segments
- **Multi-platform Analysis:** Include Reddit, YouTube, forums for 
comprehensive view

---

**Final Assessment:**

The RTX 40 series represents a **technical success but market perception 
challenge**. While Nvidia delivered industry-leading performance in 
flagship models, budget and mid-range offerings failed to meet consumer 
expectations for value and features.

The data conclusively shows that:
- **High-end market:** Satisfied (4090/4080 praised)
- **Mid-range market:** Mixed reception (4070 Ti adequate, 4070 
questioned)
- **Budget market:** Strongly negative (4060 Ti/4060 widely criticized)

For RTX 50 series success, Nvidia must address the value proposition in 
sub-$500 segment, increase VRAM allocations, and ensure feature parity 
across product stack. The emerging market engagement data suggests 
significant untapped potential if pricing and availability concerns are 
addressed.

The polarized sentiment—simultaneous high positive and elevated negative 
scores—indicates a fractured market where Nvidia excels at the premium end 
but struggles to deliver compelling budget options. Correcting this 
imbalance should be the primary focus for next-generation product 
planning.

---

## 🛠️ Technologies & Tools

### Data Collection
- Selenium WebDriver for automated scraping
- Python requests library
- Twitter/X API integration

### Data Processing
- **Languages:** Python 3.8+
- **Libraries:** Pandas, NumPy, NLTK
- **ML Framework:** PyTorch, Transformers (BERT)
- **Database:** PostgreSQL for data storage

### Analysis
- **SQL:** Complex queries for sentiment aggregation
- **NLP:** BERT-based sentiment classification
- **Visualization:** Matplotlib, Seaborn, Tableau

### Development Environment
- Jupyter Notebooks for exploratory analysis
- Git for version control
- Virtual environment for dependency management

---

## 📦 Installation & Setup

### Prerequisites
- Python 3.8 or higher
- pip package manager
- Virtual environment (recommended)

### Installation Steps

1. **Clone the repository**
```bash
git clone https://github.com/pisaevv/Big-Data-Analytics.git
cd Big-Data-Analytics
```

2. **Create virtual environment**
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install pandas numpy nltk transformers torch scikit-learn selenium
```

4. **Download NLTK data**
```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```

5. **Run preprocessing notebook**
```bash
jupyter notebook Preprocessing.ipynb
```

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for 
details.

---

## 🎓 Academic Context

This project demonstrates advanced big data analytics techniques 
including:
- Large-scale web scraping and data collection
- Natural language processing and sentiment analysis
- Statistical analysis with weighted metrics
- Geographic market segmentation
- Machine learning model preparation (BERT)
- SQL-based data aggregation
- Data visualization and insight generation

Perfect for portfolio demonstration of data science, NLP, and market 
research capabilities.

---

*Analyzing market sentiment to drive better product decisions*
