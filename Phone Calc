from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.textinput import TextInput
from kivy.uix.button import Button
import math

class PositionSizingCalculator(BoxLayout):

    def calculate_trade_parameters(self):
        try:
            account_balance = float(self.account_balance_entry.text)
            desired_risk_per_trade = float(self.desired_risk_entry.text)
            stop_loss_percent = float(self.stop_loss_percent_entry.text)
            total_fees = float(self.total_fees_entry.text)

            required_leverage = math.ceil(desired_risk_per_trade / stop_loss_percent)
            adjusted_position_size = ((account_balance * desired_risk_per_trade) / (stop_loss_percent * required_leverage + total_fees)) * required_leverage
            adjusted_position_size = min(adjusted_position_size, account_balance * required_leverage)

            self.result_label.text = f"Required Leverage: {required_leverage}x\nAdjusted Position Size: ${adjusted_position_size:.2f}"
        
        except ValueError:
            self.result_label.text = "Invalid input. Please enter numbers only."

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.orientation = 'vertical'

        self.account_balance_entry = TextInput(text='0', multiline=False)
        self.desired_risk_entry = TextInput(text='0', multiline=False)
        self.stop_loss_percent_entry = TextInput(text='0', multiline=False)
        self.total_fees_entry = TextInput(text='0', multiline=False)
        self.result_label = Label(text='')

        self.add_widget(Label(text='Account Balance:'))
        self.add_widget(self.account_balance_entry)
        self.add_widget(Label(text='Desired Risk (%):'))
        self.add_widget(self.desired_risk_entry)
        self.add_widget(Label(text='Stop Loss (%):'))
        self.add_widget(self.stop_loss_percent_entry)
        self.add_widget(Label(text='Total Fees (%):'))
        self.add_widget(self.total_fees_entry)
        calculate_button = Button(text='Calculate')
        calculate_button.bind(on_press=lambda instance: self.calculate_trade_parameters())
        self.add_widget(calculate_button)
        self.add_widget(self.result_label)

class MyApp(App):
    def build(self):
        return PositionSizingCalculator()

if __name__ == '__main__':
    MyApp().run()

