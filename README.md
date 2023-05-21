from kivy.app import App
from kivy.uix.gridlayout import GridLayout
from kivy.uix.label import Label
from kivy.uix.image import Image
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from kivy.uix.floatlayout import FloatLayout
from kivy.uix.actionbar import ActionBar, ActionButton
from kivy.uix.popup import Popup
from kivy.core.window import Window
from kivy.core.audio import SoundLoader
import cohere
co = cohere.Client('MYWu814nAU5Yp0KQdlS6GZGi49Q8Ao8CDTp4lLdA')
Window.clearcolor=255/255.0,226/255.0,165/255.0,1


# App class
class StoryApp(App):

    # Build Method
    def build(self):
        # Main Layout
        layout = FloatLayout(
        )

        # Action bar

        self.ActionBar = ActionBar(
            background_color="00FF00",
            size_hint=(1, 1),
            pos_hint={"top": 1},
        )


        # Logo widget

        self.Logo = Image(
            source=r"C:\Users\ma.alshathri\Documents\photo\pp.jpg",
            size_hint=(0.3, 0.7),
            pos_hint={"center_x": 0.5, "center_y": 0.72},

        )

        # character Text widget
        self.character = Label(
            text="[b]Enter your favorite character[/b]",
            font_size=22,
            color='#000000',
            halign="center",
            size_hint=(0.5, 0.5),
            markup=True,
            pos_hint={"center_x": 0.12, "center_y": 0.45}
        )
        # Name Text widget
        self.Name = Label(
            text="[b]Enter your name[/b]",
            font_size=22,
            color='#000000',
            halign="center",
            size_hint=(0.5, 0.5),
            markup=True,
            pos_hint={"center_x": 0.07, "center_y": 0.4}
        )

        # character Input widget
        self.CharField = TextInput(
            multiline=False,
            halign="center",
            background_color="#FFFFFF",
            foreground_color="#000000",
            cursor_color="00FF00",
            size_hint=(0.15, None),
            height="30dp",
            pos_hint={"center_x": 0.317, "center_y": 0.45}
        )
        # Name Input widget
        self.NamField = TextInput(
            multiline=False,
            halign="center",
            background_color="#FFFFFF",
            foreground_color="#000000",
            cursor_color="00FF00",
            size_hint=(0.15, None),
            height="30dp",
            pos_hint={"center_x": 0.317, "center_y": 0.39}
        )
        # Story Field widget
        self.Story = TextInput(
            multiline=True,
            halign="left",
            background_color="#FFFFFF",
            foreground_color="#000000",
            cursor_color="00FF00",
            size_hint=(0.99, None),
            height="200dp",
            pos_hint={"center_x": 0.5, "center_y": 0.18}
        )



        # Create Story Button widget
        self.StarButtom = Button(
            text="Create Your Story",
            size_hint=(0.2, None),
            height="40dp",
            pos_hint={"center_x": 0.55, "center_y": 0.42},
            bold=True,
            background_color='#00FF00',
            on_press=self.start

        )
        self.playbutton=Button(
            text="Play Sound",
            size_hint=(0.1, None),
            height="20dp",
            pos_hint={"center_x": 0.8, "center_y": 0.4},
            bold=True,
            background_color='#00FF00',
            on_press=self.PlayAudio)

        self.stopbutton=Button(
            text="Stop",
            size_hint=(0.1, None),
            height="20dp",
            pos_hint={"center_x": 0.9, "center_y": 0.4},
            bold=True,
            background_color='#00FF00',
            on_press=self.StopAudio)

        self.soundlab = Label(
            text="[b]Wanna hear a voice?[/b]",
            font_size=22,
            color='#000000',
            halign="center",
            size_hint=(0.5, 0.5),
            markup=True,
            pos_hint={"center_x": 0.85, "center_y": 0.45})
        # Add widgets
        layout.add_widget(self.ActionBar)
        layout.add_widget(self.Logo)
        layout.add_widget(self.character)
        layout.add_widget(self.Name)
        layout.add_widget(self.CharField)
        layout.add_widget(self.NamField)
        layout.add_widget(self.Story)
        layout.add_widget(self.StarButtom)
        layout.add_widget(self.stopbutton)
        layout.add_widget(self.playbutton)
        layout.add_widget(self.soundlab)

        self.sound = SoundLoader.load(r"C:\Users\ma.alshathri\Documents\photo\hello.mp3")




        # Return home Layout
        return layout

    def start(self, *args):
        response = co.generate(
            model='command-nightly',
            prompt='write a story about ' + self.CharField.text + ' and ' + self.NamField.text,
            max_tokens=200,
            temperature=0.750, )

        story = str(response)


        self.Story.text = story[115:]
    def PlayAudio(self,*args):
        self.sound.play()

    def StopAudio(self,*args):
        self.sound.stop()
# Run
StoryApp().run()

<!---
RaMq63/RaMq63 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
