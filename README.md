import pandas as pd
import numpy as np
import random
from faker import Faker

# Initialize Faker
fake = Faker()

# Number of records
n = 500000

# Lookup values
departments = ["Cardiology", "Orthopedics", "Neurology", "Oncology", "Pediatrics", "General Surgery", "Gynecology"]
procedures = ["Bypass Surgery", "Knee Replacement", "Brain Tumor Removal", "Chemotherapy", "Appendectomy", "C-Section"]
equipments = ["ECG Machine", "X-Ray", "Ventilator", "Defibrillator", "Surgical Robot", "Dialysis Machine"]
equipment_types = ["Monitoring", "Imaging", "Surgical Tool", "Life Support"]
manufacturers = ["GE Healthcare", "Siemens", "Philips", "Medtronic", "Johnson & Johnson"]
anesthesia_types = ["General", "Local", "Regional"]
operation_types = ["Major", "Minor", "Emergency", "Elective"]
complications = ["None", "Infection", "Bleeding", "Organ Failure", "Respiratory Issues"]
insurance_providers = ["Aetna", "United Health", "Blue Cross", "Cigna", "Kaiser Permanente"]

# Generate dataset
data = {
    # Patient (ID + attributes)
    "PatientID": np.random.randint(1000, 20000, n),
    "PatientName": [fake.name() for _ in range(n)],
    "Gender": np.random.choice(["Male", "Female"], n),
    "Age": np.random.randint(1, 90, n),

    # Doctor
    "DoctorID": np.random.randint(100, 500, n),
    "DoctorName": [fake.name() for _ in range(n)],
    "Specialty": np.random.choice(departments, n),
    "ExperienceYears": np.random.randint(1, 40, n),

    # Hospital
    "HospitalID": np.random.randint(1, 50, n),
    "HospitalName": [fake.company() for _ in range(n)],
    "City": [fake.city() for _ in range(n)],
    "AccreditationLevel": np.random.choice(["A", "B", "C"], n),

    # Department
    "DepartmentID": np.random.randint(10, 100, n),
    "DepartmentName": np.random.choice(departments, n),
    "Floor": np.random.randint(1, 10, n),
    "HeadDoctorName": [fake.name() for _ in range(n)],

    # Procedure
    "ProcedureID": np.random.randint(1000, 2000, n),
    "ProcedureName": np.random.choice(procedures, n),
    "ProcedureType": np.random.choice(operation_types, n),
    "AverageDuration": np.random.randint(30, 300, n),

    # Equipment
    "EquipmentID": np.random.randint(5000, 7000, n),
    "EquipmentName": np.random.choice(equipments, n),
    "EquipmentType": np.random.choice(equipment_types, n),
    "Manufacturer": np.random.choice(manufacturers, n),

    # Medical
    "MedicalID": np.random.randint(9000, 12000, n),
    "DiagnosisCode": [fake.lexify(text="???-###") for _ in range(n)],  # ICD-like code
    "InsuranceProvider": np.random.choice(insurance_providers, n),
    "PolicyNumber": [fake.bothify(text="POL####??") for _ in range(n)],

    # Date Info
    "DateID": np.arange(1, n+1),
    "OperationDate": [fake.date_between(start_date="-2y", end_date="today") for _ in range(n)],
    "DayOfWeek": np.random.choice(["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"], n),
    "Month": np.random.randint(1, 13, n),

    # Operation Facts
    "AnesthesiaType": np.random.choice(anesthesia_types, n),
    "OperationType": np.random.choice(operation_types, n),
    "DurationMinutes": np.random.randint(30, 600, n),
    "OperationCost": np.random.randint(5000, 200000, n),
    "ComplicationsFlag": np.random.choice(["Yes", "No"], n, p=[0.1, 0.9]),
    "SuccessFlag": np.random.choice(["Yes", "No"], n, p=[0.92, 0.08])
}

# Create DataFrame
df = pd.DataFrame(data)

# Save single CSV file
df.to_csv("Fact_Operations.csv", index=False)

print("✅ Fact_Operations.csv generated with", n, "records and", df.shape[1], "columns.")
