import math


def calculate_wind_chill(temp_f, wind_speed):
    if wind_speed <= 3:
        return temp_f

    return 35.74 + 0.6125 * temp_f + (0.4275 * temp_f - 35.75) * math.pow(wind_speed, 0.16)


def main():
    input_filename = '1.WCData.txt'
    output_filename = '1.WindChillReport.txt'

    with open(input_filename, 'r') as f:
        lines = f.readlines()

    data_lines = lines[2:]

    results = []
    total_adjusted_temp = 0
    observation_count = 0

    for line in data_lines:
        if line.strip():
            parts = line.strip().split()
            time = parts[0]
            temp_f = int(parts[1])
            wind_speed = int(parts[2])

            wc_temp = calculate_wind_chill(temp_f, wind_speed)
            wc_effect = wc_temp - temp_f

            wc_temp_rounded = round(wc_temp, 1)
            wc_effect_rounded = round(wc_effect, 1)

            results.append((time, wc_temp_rounded, wc_effect_rounded))
            total_adjusted_temp += wc_temp_rounded
            observation_count += 1

    average_temp = round(total_adjusted_temp / observation_count, 1) if observation_count > 0 else 0

    with open(output_filename, 'w') as f:
        f.write("Time    WC temp WC Effect\n")

        for time, wc_temp, wc_effect in results:
            f.write(f"{time}   {wc_temp:<7.1f} {wc_effect:<8.1f}\n")

        f.write(f"\nThe average adjusted temperature, based on {observation_count} observations, was {average_temp}.\n")

    print("Time    WC temp WC Effect")
    for time, wc_temp, wc_effect in results:
        print(f"{time}   {wc_temp:<7.1f} {wc_effect:<8.1f}")
    print(f"\nThe average adjusted temperature, based on {observation_count} observations, was {average_temp}.")


if __name__ == "__main__":
    main()
