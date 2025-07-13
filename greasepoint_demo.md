# greasepoint_demo.py
# A demo script for Greasepoint – Automotive Service Advisor Assistant
# Created by Phaedra Shea Drawdy

def greasepoint_assist(complaint):
    # Basic keyword mapping – extendable later
    logic_tree = {
        "grinding": {
            "concern": "Grinding noise during braking",
            "causes": [
                "Rear brake pads worn to backing plate (metal-on-metal)",
                "Scored or rusted rotors",
                "Stuck caliper piston or slide pins",
                "Debris between pad and rotor",
                "Dust shield contact"
            ],
            "steps": [
                "Visual inspection of rear brake components",
                "Measure pad thickness and rotor condition",
                "Check caliper operation"
            ],
            "ro_note": "Customer reports grinding noise when braking. Inspect rear pads, rotors, and caliper operation for metal-on-metal contact.",
            "priority": "HIGH – Safety-critical"
        },
        "clunk": {
            "concern": "Clunk noise during low-speed turns",
            "causes": [
                "CV joint wear or failure",
                "Loose sway bar links or lower control arm",
                "Strut mount or spring shift",
                "Engine/transmission mount play"
            ],
            "steps": [
                "Inspect CV axles for boot tears or play",
                "Check front suspension components",
                "Check engine and transmission mounts"
            ],
            "ro_note": "Customer reports clunk when turning left. Inspect CV joints and suspension components for looseness or wear.",
            "priority": "MEDIUM – Suspension risk"
        },
        "hesitates": {
            "concern": "Hesitation and jerking during acceleration",
            "causes": [
                "Ignition coil or spark plug misfire",
                "Throttle body or MAF sensor issues",
                "Transmission hesitation or torque converter shudder",
                "Fuel injector or pump inconsistency"
            ],
            "steps": [
                "Scan OBD-II codes",
                "Inspect ignition and fuel systems",
                "Road test vehicle with live data logging"
            ],
            "ro_note": "Customer reports hesitation when accelerating. Scan for codes and inspect ignition/fuel systems.",
            "priority": "MEDIUM-HIGH – May worsen over time"
        }
    }

    for keyword, data in logic_tree.items():
        if keyword in complaint.lower():
            return data
    
    return {
        "concern": "Unrecognized symptom – further clarification needed.",
        "causes": [],
        "steps": [],
        "ro_note": "Unable to determine specific concern from input. Recommend follow-up questions or test drive.",
        "priority": "UNKNOWN"
    }

# Example usage
if __name__ == "__main__":
    complaint_input = input("Enter customer complaint: ")
    result = greasepoint_assist(complaint_input)

    print("\n--- GREASEPOINT DIAGNOSTIC OUTPUT ---")
    print(f"Concern: {result['concern']}")
    print("\nPossible Causes:")
    for cause in result['causes']:
        print(f"- {cause}")
    
    print("\nNext Steps:")
    for step in result['steps']:
        print(f"- {step}")
    
    print(f"\nRecommended RO Note:\n{result['ro_note']}")
    print(f"\nPriority: {result['priority']}")
