 
import kivy  
from kivy.app import App  
from kivy.uix.label import Label  
from kivy.uix.textinput import TextInput  
from kivy.uix.button import Button  
  
class QuizApp(App):  
    def build(self):  
        self.score = 0  
        self.questions = [  
            {"question": "Who is Prashant's friend?", "answer": "ashwani"},  
            {"question": "What is 2 + 2?", "answer": "4"},  
            {"question": "What is the capital of Jhansi?", "answer": "Pal Colony"}  
        ]  
        self.current_question = 0  
  
        self.layout = kivy.uix.boxlayout.BoxLayout(orientation='vertical')  
        self.question_label = Label(text=self.questions[self.current_question]["question"])  
        self.answer_input = TextInput(multiline=False)  
        self.submit_button = Button(text='Submit')  
        self.score_label = Label(text='Score: 0')  
  
        self.layout.add_widget(self.question_label)  
        self.layout.add_widget(self.answer_input)  
        self.layout.add_widget(self.submit_button)  
        self.layout.add_widget(self.score_label)  
  
        self.submit_button.bind(on_press=self.check_answer)  
  
        return self.layout  
  
    def check_answer(self, instance):  
        user_answer = self.answer_input.text.lower()  
        if user_answer == self.questions[self.current_question]["answer"].lower():  
            self.score += 1  
            self.score_label.text = f'Score: {self.score}'  
            self.question_label.text = 'Correct!'  
        else:  
            self.question_label.text = f'Incorrect. The correct answer is {self.questions[self.current_question]["answer"]}'  
  
        self.current_question += 1  
        if self.current_question >= len(self.questions):  
            self.question_label.text = 'Quiz complete!'  
            self.answer_input.disabled = True  
            self.submit_button.disabled = True  
  
if __name__ == '__main__':  
    QuizApp().run()  
