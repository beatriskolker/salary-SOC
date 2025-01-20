def calculate_monthly_earnings():
    # Define rates and multipliers
    base_hourly_rate = 70  # Base hourly rate
    shift_rates = {
        "night": 1.25 * base_hourly_rate,  # 125% of base rate
        "weekend": 1.4 * base_hourly_rate,  # 140% of base rate
        "normal": base_hourly_rate  # Normal shifts
    }

    # Ask user for input
    print("Enter your shifts for the month in the following format:")
    print("Example: night:2, weekend:1, normal:5")
    print("Type 'done' to finish.")

    shifts_input = input("\nEnter all shifts: ").lower()
    total_earnings = 0

    if shifts_input != "done":
        # Split input into individual shift entries
        shifts = shifts_input.split(",")

        for shift in shifts:
            try:
                # Split each entry into type and count
                shift_type, num_shifts = shift.split(":")
                num_shifts = int(num_shifts.strip())  # Convert count to integer

                if shift_type.strip() in shift_rates:
                    # Calculate earnings for this shift type
                    shift_earning = (shift_rates[shift_type.strip()] * 8) * num_shifts
                    total_earnings += shift_earning
                else:
                    print(f"Invalid shift type: {shift_type}. Skipping...")
            except ValueError:
                print(f"Invalid entry format: {shift}. Skipping...")

    # Ask if all shifts were worked in the month
    all_shifts_answer = input("\nDid you work all your shifts this month? (yes/no) (adds 225 shekels for bus ticket payment): ").lower()
    if all_shifts_answer == "yes":
        total_earnings += 225  # Add payment for bus tickets

    print(f"\nTotal monthly earnings: {total_earnings} shekels")

# Run the function
calculate_monthly_earnings()
