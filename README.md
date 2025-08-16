import pandas as pd
import numpy as np
import random
from faker import Faker

# Initialize Faker
fake = Faker()

# Number of records
n = 500000

# Sample lookup values
departments = ["Cardiology", "Orthopedics", "Neurology", "Oncology", "Pediatrics", "General Surgery", "Gynecology"]
procedures = ["Bypass Surgery", "Knee Replacement", "Brain Tumor Removal", "Chemotherapy", "Appendectomy", "C-Section"]
anesthesia_types = ["General", "Local", "Regional"]
operation_types = ["Major", "Minor", "Emergency", "Elective"]
complications = ["None", "Infection", "Bleeding", "Organ Failure", "Respiratory Issues"]

# Generate dataset
data = {
    "OperationID": np.arange(1, n+1),
    "PatientID": np.random.randint(1000, 20000, n),
    "DoctorID": np.random.randint(100, 500, n),
    "AssistantDoctorID": np.random.randint(500, 800, n),
    "HospitalID": np.random.randint(1, 50, n),
    "Department": np.random.choice(departments, n),
    "Procedure": np.random.choice(procedures, n),
    "OperationDate": [fake.date_between(start_date="-2y", end_date="today") for _ in range(n)],
    "DischargeDate": [fake.date_between(start_date="-2y", end_date="today") for _ in range(n)],
    "OperationRoomNumber": np.random.randint(1, 50, n),
    "OperationType": np.random.choice(operation_types, n),
    "AnesthesiaType": np.random.choice(anesthesia_types, n),
    "SurgicalTeamCount": np.random.randint(3, 10, n),
    "EquipmentUsedID": np.random.randint(1000, 5000, n),
    "ImplantUsedFlag": np.random.choice(["Yes", "No"], n),
    "BloodUnitsUsed": np.random.randint(0, 5, n),
    "DurationMinutes": np.random.randint(30, 600, n),
    "PreOpDiagnosis": [fake.word() for _ in range(n)],
    "PostOpDiagnosis": [fake.word() for _ in range(n)],
    "OperationCost": np.random.randint(5000, 200000, n),
    "InsuranceCoverage": np.random.randint(1000, 150000, n),
    "PatientPayable": np.random.randint(500, 50000, n),
    "MedicationCost": np.random.randint(1000, 30000, n),
    "EquipmentCost": np.random.randint(500, 20000, n),
    "ComplicationsFlag": np.random.choice(["Yes", "No"], n),
    "ComplicationType": np.random.choice(complications, n),
    "SuccessFlag": np.random.choice(["Yes", "No"], n, p=[0.9, 0.1]),
    "MortalityFlag": np.random.choice(["Yes", "No"], n, p=[0.98, 0.02]),
    "ReadmissionFlag": np.random.choice(["Yes", "No"], n, p=[0.85, 0.15]),
    "RecoveryDays": np.random.randint(1, 60, n)
}

# Create DataFrame
df = pd.DataFrame(data)

# Save to CSV
df.to_csv("Fact_PatientOperations.csv", index=False)

print("✅ Fact_PatientOperations.csv generated with", n, "records.")
