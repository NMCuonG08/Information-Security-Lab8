## Prepare

![image](https://github.com/user-attachments/assets/d89eb74d-a2aa-4b2b-9c04-c15de1b89a95)

```python
import matplotlib.pyplot as plt
from collections import Counter

# Tần suất thực tế của các chữ cái và bigrams trong tiếng Anh
real_frequencies = {
    'E': 12.70, 'T': 9.06, 'A': 8.17, 'O': 7.51, 'I': 6.97, 'N': 6.75, 'S': 6.33,
    'H': 6.09, 'R': 5.99, 'D': 4.25, 'L': 4.03, 'C': 2.78, 'U': 2.76, 'M': 2.41,
    'P': 2.14, 'B': 2.03, 'V': 1.97, 'K': 1.29, 'J': 0.15, 'X': 0.15, 'Q': 0.10,
    'Z': 0.07, 'Y': 0.19, 'W': 0.23, 'F': 0.22
}

real_bigrams = {
    'TH': 3.8, 'HE': 3.2, 'IN': 2.7, 'ER': 2.5, 'AN': 2.4, 'RE': 2.3, 'ND': 2.3,
    'AT': 2.2, 'ON': 2.2, 'EN': 2.1, 'ED': 2.0, 'TO': 1.9, 'OR': 1.8, 'IT': 1.7,
    'IS': 1.7
}

# Phân tích tần suất cho các chữ cái trong văn bản chuẩn tiếng Anh
def letter_frequency_analysis(text):
    filtered_text = ''.join([c for c in text if c.isalpha()]).upper()
    frequencies = Counter(filtered_text)
    return frequencies

# Phân tích tần suất cho các bigrams trong văn bản chuẩn tiếng Anh
def bigram_frequency_analysis(text):
    filtered_text = ''.join([c for c in text if c.isalpha()]).upper()
    bigrams = [filtered_text[i:i+2] for i in range(len(filtered_text)-1)]
    frequencies = Counter(bigrams)
    return frequencies

# Giả sử bạn có một văn bản chuẩn nào đó, ví dụ văn bản tiếng Anh phổ biến
text = """
The quick brown fox jumps over the lazy dog. This is an example sentence to show letter and bigram frequencies.
"""

# Phân tích tần suất trong văn bản chuẩn
letter_freqs = letter_frequency_analysis(text)
bigram_freqs = bigram_frequency_analysis(text)

# Vẽ biểu đồ so sánh tần suất các chữ cái (letters)
plt.figure(figsize=(12, 6))
plt.bar(real_frequencies.keys(), [real_frequencies.get(k, 0) for k in real_frequencies.keys()],
        label='Real English', color='salmon', width=0.35)
plt.bar(letter_freqs.keys(), [letter_freqs.get(k, 0) for k in real_frequencies.keys()],
        label='Sample Text', color='skyblue', width=0.35)
plt.title("Comparison of Letter Frequencies", fontsize=16)
plt.xlabel("Letters", fontsize=14)
plt.ylabel("Frequency (%)", fontsize=14)
plt.xticks(rotation=45, ha='right', fontsize=12)
plt.legend()
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()

# Vẽ biểu đồ so sánh tần suất các bigrams
plt.figure(figsize=(12, 6))
plt.bar(real_bigrams.keys(), [real_bigrams.get(k, 0) for k in real_bigrams.keys()],
        label='Real English', color='salmon', width=0.35)
plt.bar(bigram_freqs.keys(), [bigram_freqs.get(k, 0) for k in real_bigrams.keys()],
        label='Sample Text', color='skyblue', width=0.35)
plt.title("Comparison of Bigram Frequencies", fontsize=16)
plt.xlabel("Bigrams", fontsize=14)
plt.ylabel("Frequency (%)", fontsize=14)
plt.xticks(rotation=45, ha='right', fontsize=12)
plt.legend()
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()

```

![image](https://github.com/user-attachments/assets/981d7299-9faa-449c-ac0b-87acbc7dfaec)

![image](https://github.com/user-attachments/assets/e06e5645-9b89-4125-a6a8-ba22f414c8b6)

```python
from collections import Counter
import matplotlib.pyplot as plt

# Ciphertext
ciphertext = """
THVVWCZTQ!
CZ WECQ YIAQQ, LFN JCII IVAHZ WEV DCPPVHVZYV MVWJVVZ VZYHLOWCFZ AZD
ANWEVZWCYAWCFZ. WECQ RVQQATV CQ VZYHLOWVD JCWE A BVHL CZQVYNHV
VZYHLOWCFZ QYEVRV. CDVAIIL, AZ VZYHLOWCFZ QYEVRV QEFNID AIIFJ FZIL
ANWEFHCGVD OAHWCVQ, JEF XZFJ WEV XVL, WF HVAD WEV RVQQATV. EFJVBVH,
LFN SNQW HVAD WEV RVQQATV JCWEFNW XZFJCZT WEV XVL. EVZYV, WEV
VZYHLOWCFZ QYEVRV CQ CZQVYNHV.
"""

# Frequency analysis function
def frequency_analysis(text):
    filtered_text = ''.join([c for c in text if c.isalpha()])  # Only letters
    frequencies = Counter(filtered_text)
    return frequencies

# Perform frequency analysis
freqs = frequency_analysis(ciphertext)

# Sort frequencies by letter
sorted_freqs = dict(sorted(freqs.items(), key=lambda item: item[1], reverse=True))

# Plot the frequencies
plt.figure(figsize=(10, 6))
plt.bar(sorted_freqs.keys(), sorted_freqs.values(), color='skyblue')
plt.title("Frequency of Letters in Ciphertext", fontsize=16)
plt.xlabel("Letters", fontsize=14)
plt.ylabel("Frequency", fontsize=14)
plt.xticks(fontsize=12)
plt.yticks(fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

```


![image](https://github.com/user-attachments/assets/3f556633-7570-4ed1-abbb-e83825e71d2c)



```python
from collections import Counter
import matplotlib.pyplot as plt

# Ciphertext
ciphertext = """
THVVWCZTQ!
CZ WECQ YIAQQ, LFN JCII IVAHZ WEV DCPPVHVZYV MVWJVVZ VZYHLOWCFZ AZD
ANWEVZWCYAWCFZ. WECQ RVQQATV CQ VZYHLOWVD JCWE A BVHL CZQVYNHV
VZYHLOWCFZ QYEVRV. CDVAIIL, AZ VZYHLOWCFZ QYEVRV QEFNID AIIFJ FZIL
ANWEFHCGVD OAHWCVQ, JEF XZFJ WEV XVL, WF HVAD WEV RVQQATV. EFJVBVH,
LFN SNQW HVAD WEV RVQQATV JCWEFNW XZFJCZT WEV XVL. EVZYV, WEV
VZYHLOWCFZ QYEVRV CQ CZQVYNHV.
"""

# Frequency analysis function for bigrams
def bigram_frequency_analysis(text):
    # Filter out non-alphabetic characters and convert to uppercase
    filtered_text = ''.join([c for c in text if c.isalpha()]).upper()
    
    # Generate bigrams (pairs of two consecutive letters)
    bigrams = [filtered_text[i:i+2] for i in range(len(filtered_text)-1)]
    
    # Calculate frequency of each bigram
    frequencies = Counter(bigrams)
    return frequencies

# Perform bigram frequency analysis
bigram_freqs = bigram_frequency_analysis(ciphertext)

# Sort frequencies by bigram
sorted_bigram_freqs = dict(sorted(bigram_freqs.items(), key=lambda item: item[1], reverse=True))

# Take only the top 20 bigrams
top_20_bigrams = dict(list(sorted_bigram_freqs.items())[:20])

# Plot the frequencies of top 20 bigrams
plt.figure(figsize=(12, 6))
plt.bar(top_20_bigrams.keys(), top_20_bigrams.values(), color='skyblue')
plt.title("Top 20 Most Frequent Bigrams in Ciphertext", fontsize=16)
plt.xlabel("Bigrams", fontsize=14)
plt.ylabel("Frequency", fontsize=14)
plt.xticks(rotation=45, ha='right', fontsize=12)  # Rotate x-axis labels for better readability
plt.yticks(fontsize=12)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()

```




![image](https://github.com/user-attachments/assets/a24637b6-6fb3-427d-b86d-56ddbddfd60d)




# Replace character

```python
# Ciphertext ban đầu
ciphertext = """
THVVWCZTQ!
CZ WECQ YIAQQ, LFN JCII IVAHZ WEV DCPPVHVZYV MVWJVVZ VZYHLOWCFZ AZD
ANWEVZWCYAWCFZ. WECQ RVQQATV CQ VZYHLOWVD JCWE A BVHL CZQVYNHV
VZYHLOWCFZ QYEVRV. CDVAIIL, AZ VZYHLOWCFZ QYEVRV QEFNID AIIFJ FZIL
ANWEFHCGVD OAHWCVQ, JEF XZFJ WEV XVL, WF HVAD WEV RVQQATV. EFJVBVH,
LFN SNQW HVAD WEV RVQQATV JCWEFNW XZFJCZT WEV XVL. EVZYV, WEV
VZYHLOWCFZ QYEVRV CQ CZQVYNHV.
"""



# Bản đồ thay thế thủ công (dựa trên tần suất)
mapping = {
    'V': 'E', 
    'W':'T',

}

# Hàm thay thế thủ công các chữ cái trong ciphertext, giữ nguyên dấu câu
def manual_substitution(text, mapping):
    decoded_text = []
    for char in text:
        if char.upper() in mapping:  # Nếu ký tự có trong bản đồ
            # Kiểm tra xem ký tự có phải là chữ hoa không
            if char.isupper():
                decoded_text.append(mapping[char.upper()])
            else:
                decoded_text.append(mapping[char.upper()].lower())
        elif char.isalpha():
            # Nếu ký tự là chữ cái nhưng không có trong bản đồ, thay bằng dấu "."
            decoded_text.append('.')
        else:
            # Giữ nguyên các ký tự không phải chữ cái (dấu câu, khoảng trắng)
            decoded_text.append(char)
    
    return ''.join(decoded_text)

# Áp dụng thay thế thủ công
decoded_text = manual_substitution(ciphertext, mapping)

# In kết quả đã được thay thế
print("Decoded Text:")
print(decoded_text)

```

















