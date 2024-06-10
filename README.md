# Learn-Spring-boot

import random
import json

# Sample data
industry_sectors = ["Agriculture", "Mining", "Utilities", "Construction", "Manufacturing",
                    "Wholesale Trade", "Retail Trade", "Transportation", "Information",
                    "Finance", "Real Estate", "Professional Services", "Management", 
                    "Administrative", "Educational Services", "Health Care", "Arts", 
                    "Accommodation", "Other Services", "Public Administration"]

# Divide into 4 related sections
sections = [
    industry_sectors[0:5],  # Section 1: Agriculture to Manufacturing
    industry_sectors[5:10], # Section 2: Wholesale Trade to Finance
    industry_sectors[10:15],# Section 3: Real Estate to Educational Services
    industry_sectors[15:20] # Section 4: Health Care to Public Administration
]

def generate_wcustomer_id():
    return f"W{random.randint(100000, 999999)}"

def generate_duns_number():
    return f"{random.randint(100000000, 999999999)}"

# Generate unique IDs
wcustomer_ids = set()
duns_numbers = set()

while len(wcustomer_ids) < 100:
    wcustomer_ids.add(generate_wcustomer_id())

while len(duns_numbers) < 100:
    duns_numbers.add(generate_duns_number())

# Convert sets to lists for easy indexing
wcustomer_ids = list(wcustomer_ids)
duns_numbers = list(duns_numbers)

# Create the JSON structure
data = []

# Loop over each NAICS industry and generate entries
for i, industry in enumerate(industry_sectors):
    # Pick a section for the mapping industry
    section = sections[i // 5]
    related_industries = [ind for ind in section if ind != industry]
    
    customer_ids = [wcustomer_ids.pop() for _ in range(5)]
    duns_numbers = [duns_numbers.pop() for _ in range(5)]
    
    entry = {
        "NAICS Industry": industry,
        "Customer IDs": customer_ids,
        "Duns Numbers": duns_numbers,
        "Mapping Industries": related_industries
    }
    data.append(entry)

# Convert to JSON
json_data = json.dumps(data, indent=4)

# Print the JSON data
print(json_data)
