# DQN-car-track — Quick Test README

This repo contains a small test harness that loads a pre-trained DQN model and runs it on a simple car/track environment (rendered with Pygame). 

## 1) Clone the repo

```bash
git clone https://github.com/AbdulwahhabAli/DQN-car-track.git
cd DQN-car-track
```

## 2) (Recommended) Create and activate a virtual environment

```bash
python3 -m venv .venv
# source .venv/bin/activate  # on macOS/Linux
# .venv\Scripts\activate   # on Windows (PowerShell)
```

## 3) Install dependencies

> If the repo includes a `requirements.txt`, do:
```bash
pip install -r requirements.txt
```

> Notes:
> - Your log shows **Pygame 2.6.1** and **Keras (TensorFlow backend)** working on **Python 3.13**.
> - If you’re on Apple Silicon and need GPU acceleration, you can optionally install `tensorflow-metal` (Apple’s GPU plugin), but CPU works fine for this test.

## 4) Run the model test

From inside the cloned folder:

```bash
python3 main_test_model.py
```


## 5) What you should see

- A Pygame window opens showing the track and the agent.
- Console prints similar to:

```
pygame 2.6.1 (SDL 2.28.4, Python 3.13.7)
Hello from the pygame community. https://www.pygame.org/contribute.html
WARNING:absl:Compiled the loaded model, but the compiled metrics have yet to be built...
WARNING:absl:Error in loading the saved optimizer state...
1/1 ━━━━━━━━━ 0s 6ms/step
1/1 ━━━━━━━━━ 0s 6ms/step
...
```

Those `1/1 ... ms/step` lines are inference calls; seeing many of them is normal while the agent steps through the environment.

---

## Common warnings you can safely ignore for this test

- **`pkg_resources is deprecated` (from setuptools)**  
  Shown by Pygame’s `pkgdata.py`. It’s a deprecation notice and doesn’t affect running.

- **`Argument 'decay' is no longer supported` (Keras)**  
  Comes from older optimizer configs; the model still runs.

- **`Error in loading the saved optimizer state... starting with a freshly initialized optimizer`**  
  Harmless when you’re only **testing/inferencing** a saved model; optimizer state matters for continued training, not inference.

- **`Compiled metrics have yet to be built`**  
  Also fine when you’re not calling `model.evaluate()`.

---

## Troubleshooting

- **Pygame window doesn’t open (macOS):**  
  Make sure you’re not running from a headless/remote session. If you see audio/display init errors, try:
  ```bash
  export SDL_AUDIODRIVER=dummy
  ```
  and re-run.

- **TensorFlow on Python 3.13 issues:**  
  You’re already running on 3.13 per your log. If a different machine has trouble, try Python **3.10–3.12** which are commonly supported, or upgrade TF/Keras.

- **Slow frame rate:**  
  Disable other heavy apps; optionally install `tensorflow-metal` on Apple Silicon:
  ```bash
  pip install tensorflow-metal
  ```

- **No model file / wrong path:**  
  Ensure any expected saved model (e.g., `.keras` / `.h5` / SavedModel dir) is present at the path used inside `main_test_model.py`.

---

## Project layout (essentials)

```
DQN-car-track/
├─ main_test_model.py     # Entry point for the quick test
├─ (assets, model files)  # Model + env art as referenced by the script
└─ requirements.txt       # If present, use it to install deps
```

---


## License / Credits

- Environment rendering: **Pygame**  
- Deep RL agent: **Keras (TensorFlow backend)**  
- Repo: <owner: AbdulwahhabAli / project: DQN-car-track>
