# HKeducalc
mark analyser for 12th students to calculate their cutoff and pass results in exam

def get_mark(subject: str) -> int:
    while True:
        try:
            value = int(input(f"{subject}: ").strip())
        except ValueError:
            print("Please enter a whole number between 0 and 100.")
            continue

        if 0 <= value <= 100:
            return value
        print("Marks must be between 0 and 100.")


def subject_status(marks: int) -> str:
    return "Pass" if marks >= 35 else "Fail"


def calculate_cutoff(marks: dict[str, int], course: str) -> float:
    if course == "Maths":
        return marks["Maths"] + marks["Physics"] / 2 + marks["Chemistry"] / 2
    if course == "Biology":
        return marks["Biology"] + marks["Physics"] / 2 + marks["Chemistry"] / 2
    return 0.0


def main() -> None:
    print("12th Marks Calculator")
    print("Made by Harish Kumar [HK]")
    print("Enter your marks for each subject below.")
    print()

    name = input("Student name: ").strip() or "Student"
    subjects = ["Tamil", "English", "Maths", "Physics", "Chemistry", "Biology"]
    marks: dict[str, int] = {}

    for subject in subjects:
        marks[subject] = get_mark(subject)

    pass_results = {subject: subject_status(score) for subject, score in marks.items()}
    overall_pass = all(score >= 35 for score in marks.values())
    total = sum(marks.values())
    percentage = total / 600 * 100
    maths_cutoff = calculate_cutoff(marks, "Maths")
    bio_cutoff = calculate_cutoff(marks, "Biology")

    print("\n---- Result Summary ----")
    print(f"Name: {name}")
    for subject in subjects:
        print(f"{subject:9}: {marks[subject]:3}  {pass_results[subject]}")
    print(f"Total Marks: {total}/600")
    print(f"Percentage: {percentage:.2f}%")
    print(f"Overall Result: {'Pass' if overall_pass else 'Fail'}")
    print(f"Maths cutoff score: {maths_cutoff:.1f}")
    print(f"Biology cutoff score: {bio_cutoff:.1f}")

    if percentage >= 90:
        grade = "A+"
    elif percentage >= 75:
        grade = "A"
    elif percentage >= 60:
        grade = "B"
    elif percentage >= 50:
        grade = "C"
    else:
        grade = "D"

    print(f"Grade: {grade}")
    print("\nWell done! Keep studying hard.")


if __name__ == "__main__":
    main()
