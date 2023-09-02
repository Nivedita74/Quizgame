import tkinter as tk
from tkinter import messagebox

class QuizGame:
    def __init__(self, root):
        self.root = root
        self.root.title("Quiz Game")

        self.question_label = tk.Label(root, text="Question goes here")
        self.question_label.pack(pady=10)

        self.option_var = tk.StringVar()
        self.option1 = tk.Radiobutton(root, text="Option 1", variable=self.option_var, value="Option 1")
        self.option2 = tk.Radiobutton(root, text="Option 2", variable=self.option_var, value="Option 2")
        self.option3 = tk.Radiobutton(root, text="Option 3", variable=self.option_var, value="Option 3")
        self.option4 = tk.Radiobutton(root, text="Option 4", variable=self.option_var, value="Option 4")

        self.option1.pack()
        self.option2.pack()
        self.option3.pack()
        self.option4.pack()

        self.submit_button = tk.Button(root, text="Submit", command=self.check_answer)
        self.submit_button.pack(pady=10)

        self.question_number = 0
        self.score = 0

        self.questions = [
            {
                "question": "What is 2 + 2?",
                "correct_answer": "Option 1",
                "options": ["4", " 2", " 3", " 14"]
            },
            {
                "question": "Which planet is known as the Red Planet?",
                "correct_answer": "Option 2",
                "options": ["Earth", "Mars", "Sun", "Moon"]
            },
             {
                "question": "Which planet is known as the blue Planet?",
                "correct_answer": "Option 1",
                "options": ["Earth", "Mars", "Sun", "Moon"]
            },
           
            # Add more questions here
        ]

        self.load_question()

    def load_question(self):
        if self.question_number < len(self.questions):
            question = self.questions[self.question_number]
            self.question_label.config(text=question["question"])
            self.option1.config(text=question["options"][0])
            self.option2.config(text=question["options"][1])
            self.option3.config(text=question["options"][2])
            self.option4.config(text=question["options"][3])
            self.option_var.set("")
        else:
            messagebox.showinfo("Quiz Over", f"Quiz is over. Your score: {self.score}")

    def check_answer(self):
        selected_option = self.option_var.get()
        correct_answer = self.questions[self.question_number]["correct_answer"]

        if selected_option == correct_answer:
            self.score += 1

        self.question_number += 1
        self.load_question()

if __name__ == "__main__":
    root = tk.Tk()
    quiz_game = QuizGame(root)
    root.mainloop()
