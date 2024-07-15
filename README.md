# Z12import math
import sqlite3
from datetime import datetime

# Calculate the total volume of water on Earth
def calculate_total_water_volume(ocean_surface_area_km2=361100000, average_ocean_depth_m=3688):
    ocean_volume_km3 = ocean_surface_area_km2 * average_ocean_depth_m / 1000  # Convert from km²*m to km³
    return ocean_volume_km3

# Example usage of the function to calculate the total volume of water
total_water_volume = calculate_total_water_volume()
print(f"Estimated total volume of water on Earth: {total_water_volume:.2e} km³")

# Create database for cryptocurrency events
def create_database(db_name='crypto_events.db'):
    conn = sqlite3.connect(db_name)
    cursor = conn.cursor()
    cursor.execute('''
    CREATE TABLE IF NOT EXISTS events (
        id INTEGER PRIMARY KEY,
        date TEXT,
        event TEXT,
        description TEXT
    )
    ''')
    conn.commit()
    conn.close()

# Add an event to the database
def add_event(date, event, description, db_name='crypto_events.db'):
    conn = sqlite3.connect(db_name)
    cursor = conn.cursor()
    cursor.execute('''
    INSERT INTO events (date, event, description) VALUES (?, ?, ?)
    ''', (date, event, description))
    conn.commit()
    conn.close()

# Get all events from the database
def get_all_events(db_name='crypto_events.db'):
    conn = sqlite3.connect(db_name)
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM events')
    events = cursor.fetchall()
    conn.close()
    return events

# Example usage of database functions
create_database()
add_event(datetime.now().strftime("%Y-%m-%d %H:%M:%S"), 'Bitcoin Halving', 'The reward for mining new Bitcoin blocks is halved.')
events = get_all_events()
for event in events:
    print(event)
