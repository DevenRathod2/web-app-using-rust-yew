# Web-App-using-Rust-and-Yew
A Simple Web Application build using Rust and Yew Framework


# Build a simple app

<h2>Create Project</h2>
<br>

<p>To get started, create a new cargo project.</p>

<code>
cargo new yew-app
</code>

<br>
<p>Open the newly created directory.</p>

<code>
cd yew-app
</code>

# Run a hello world example

<p>
To verify the Rust environment is setup, run the initial project using the cargo build tool. After output about the build process, you should see the expected "Hello World" message.
</p>

<code>
cargo run
</code>

Converting the project into a Yew web application
To convert this simple command line application to a basic Yew web application, a few changes are needed.

Update Cargo.toml
Add yew to the list of dependencies.

Cargo.toml
[package]
name = "yew-app"
version = "0.1.0"
edition = "2018"

[dependencies]
# you can check the latest version here: https://crates.io/crates/yew
yew = "0.19"
Update main.rs
We need to generate a template which sets up a root Component called Model which renders a button that updates its value when clicked. Replace the contents of src/main.rs with the following code.

NOTE
The line yew::start_app::<Model>() inside main() starts your application and mounts it to the page's <body> tag.
If you would like to start your application with any dynamic properties, you can instead use yew::start_app_with_props::<Model>(..).

# main.rs
  
<code>
use yew::prelude::*;

enum Msg {
    AddOne,
}

struct Model {
    value: i64,
}

impl Component for Model {
    type Message = Msg;
    type Properties = ();

    fn create(_ctx: &Context<Self>) -> Self {
        Self {
            value: 0,
        }
    }

    fn update(&mut self, _ctx: &Context<Self>, msg: Self::Message) -> bool {
        match msg {
            Msg::AddOne => {
                self.value += 1;
                // the value has changed so we need to
                // re-render for it to appear on the page
                true
            }
        }
    }

    fn view(&self, ctx: &Context<Self>) -> Html {
        // This gives us a component's "`Scope`" which allows us to send messages, etc to the component.
        let link = ctx.link();
        html! {
            <div>
                <button onclick={link.callback(|_| Msg::AddOne)}>{ "+1" }</button>
                <p>{ self.value }</p>
            </div>
        }
    }
}

fn main() {
    yew::start_app::<Model>();
}
  
</code>
  
# Create index.html
Finally, add an index.html file in the root directory of your app.

# index.html
  
<code>
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Yew App</title>
  </head>
</html>
  
  </code>
View your web application
Run the following command to build and serve the application locally.

trunk serve
Trunk will helpfully rebuild your application if you modify any of its files.