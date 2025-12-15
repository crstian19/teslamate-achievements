<div align="center">
  <img src="https://cdn.crstian.me/teslamate-achievements-logo.png" alt="TeslaMate Achievements" width="200"/>




# TeslaMate Achievements Dashboard 🏆

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Grafana](https://img.shields.io/badge/Grafana-12.1.1+-orange?style=for-the-badge&logo=grafana)](https://grafana.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16+-blue?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)
[![TeslaMate](https://img.shields.io/badge/TeslaMate-Compatible-green?style=for-the-badge)](https://github.com/teslamate-org/teslamate)

*A gamification dashboard for TeslaMate that tracks and displays various driving achievements based on your Tesla vehicle data.*

[Quick Start](#-quick-start) • [Configuration](#️-configuration) • [Achievements](#-achievement-categories) • [Troubleshooting](#-troubleshooting)


  <img src="https://cdn.crstian.me/achievements-dashboard.png" alt="Achievements Dashboard" width="800"/>
</div>

---

## 📖 Overview

This dashboard transforms your Tesla driving experience into an engaging achievement system, motivating you to explore new driving habits, improve efficiency, and reach exciting milestones while tracking your environmental impact.

### ✨ Key Features

- **50+ Unique Achievements** across 10 diverse categories
- **Real-time Progress Tracking** based on your TeslaMate data
- **Visual Progress Indicators** with emoji-based status display
- **Comprehensive Categories**: Efficiency, Exploration, Performance, Ecology, and more
- **Customizable Metrics** to match your driving habits and preferences
- **Environment-focused Tracking** with CO₂ savings calculations

---

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have:

- ✅ **TeslaMate**: Fully functional instance with PostgreSQL database
- ✅ **Grafana**: Version 12.1.1 or higher with table panel support

### Installation

**Edit your Teslamate "docker-compose.yml" file and add these two new lines at the end of the "volumes" section of the grafana container:**

```yaml
services:
  grafana:
    volumes:
      - teslamate-grafana-data:/var/lib/grafana
      - ~/teslamate-achievements/dashboard.yml:/etc/grafana/provisioning/dashboards/dashboard.yml
      - ~/teslamate-achievements/dashboards:/TeslaMateAchievements
```

1. **Clone this repository** (if you haven't already):
   ```bash
   git clone https://github.com/your-username/teslamate-achievements.git ~/teslamate-achievements
   ```

2. **Save your docker-compose.yml file**

3. **Recreate Grafana container**:
   ```bash
   docker compose up -d
   ```

4. **Browse the Grafana Dashboards** from the Web and you should have a new "TeslaMate Achievements" folder

---



## ⚙️ Configuration


### Custom Car ID

Update all SQL queries in the dashboard:

```sql
-- Replace car_id = 1 with your specific car ID
WHERE car_id = 2  -- Example for second car
```

### Home Location Setup

The dashboard searches for geofences containing specific patterns:

```sql
-- Edit home location patterns in relevant queries
WHERE (g.name ILIKE '%Home%' OR g.name ILIKE '%Casa%' OR g.name ILIKE '%YourHomeName%')
```

### Energy Cost Calculations

Customize your savings calculations:

```sql
-- Modify the gas savings multiplier
(sum(distance) * 0.15) - (SELECT sum(coalesce(cost,0)) FROM charging_processes WHERE car_id=1)
--                   ^^^^ Adjust this value based on local gas prices
```

---

## 🏅 Achievement Categories

### 🌿 Efficiency & Energy
| Achievement | Requirement |
|-------------|-------------|
| **Hypermiler** | Drive >50km with >100% efficiency vs rated range |
| **Efficiency Master** | Efficiency >100% vs Rated (7-day streak) |
| **Efficiency Expert** | Efficiency >110% vs Rated (7-day streak) |
| **Efficiency Guru** | Efficiency >120% vs Rated (7-day streak) |
| **Supercharger Junkie** | Fast charge at speeds over 120 kW |

### 🌍 Exploration & Geography
| Achievement | Requirement |
|-------------|-------------|
| **Local Explorer** | Visit 5 different cities |
| **Regional Explorer** | Visit 10 different regions/counties |
| **National Explorer** | Visit 15 different states/provinces |
| **Adventurer** | Travel more than 300 km from home |
| **Globetrotter** | Travel more than 500 km from home |

### ⏱️ Time & Weather
| Achievement | Requirement |
|-------------|-------------|
| **Sub-Zero** | Charge while outside temp is below 0°C |
| **Night Rider** | Complete a drive between 02:00 AM and 05:00 AM |
| **Night Owl** | Accumulate >100 km at night (00:00-06:00) |
| **Midnight Warrior** | Accumulate >500 km at night (00:00-06:00) |
| **Early Bird** | Start 10 charging sessions before 7:00 AM |
| **Veteran** | Data collected for more than 1 year |

### 🏎️ Endurance & Performance
| Achievement | Requirement |
|-------------|-------------|
| **Iron Butt** | Drive >400km in a single trip |
| **Total Marathoner** | Accumulate >10,000 km total distance |
| **Daily Marathoner** | Drive >500 km in a single day |
| **Ultra Marathoner** | Drive >800 km in a single day |
| **Speedster** | Reach a top speed >180 km/h |
| **Smooth Operator** | 1,000 km streak without exceeding 120 km/h |

### 💰 Savings & Charging Habits
| Achievement | Requirement |
|-------------|-------------|
| **Bounty Hunter** | Charge 100 kWh for free (0 cost recorded) |
| **Freeloader** | Charge 1,000 kWh for free |
| **Night Planner** | Complete 50 charging sessions off-peak (00:00-08:00) |
| **Thrifty** | Save estimated >500€ vs Gas |
| **Green Tycoon** | Save estimated >1,000€ vs Gas |

### 🔋 Battery Tech & Strategy
| Achievement | Requirement |
|-------------|-------------|
| **Patient Lvl 1-3** | Spend 10/50/100 hours charging total |
| **AC Devotee** | 80% of charging sessions are AC (Slow) |
| **Fast Charge Pro** | Complete 100 Supercharger sessions (>50kW) |
| **Full Cycle** | Charge from <10% to >95% |
| **The Optimizer** | Finish 100 charges between 80-90% SoC |

### 🌿 Ecology & Impact
| Achievement | Requirement |
|-------------|-------------|
| **Planet Guardian** | Save 1,000 kg of CO2 vs ICE car |
| **Climate Hero** | Save 5,000 kg of CO2 vs ICE car |
| **Personal Forest** | Save CO2 equivalent to planting 50 trees |
| **Amazon Rainforest** | Save CO2 equivalent to planting 200 trees |

### 🚀 Space & Time Continuum
| Achievement | Requirement |
|-------------|-------------|
| **Around the World** | Drive 40,075 km (Earth Circumference) |
| **ISS Orbiter** | Drive 42,500 km (One ISS Orbit distance) |
| **To the Moon** | Drive 384,400 km (Earth to Moon distance) |
| **24h Le Mans** | Spend 24 total hours driving |
| **Road Tourist** | Spend 100 total hours driving |
| **A Week on the Road** | Spend 168 total hours (1 week) driving |

### 🏔️ Habits & Extremes
| Achievement | Requirement |
|-------------|-------------|
| **Daily Driver** | Drive 7/30/100 consecutive days |
| **Weekender** | 60% of driving done on weekends |
| **Workaholic** | 60% of driving done on weekdays (Mon-Fri) |
| **Inferno Rider** | Drive in temperatures >40°C |
| **Ice Road Trucker** | Drive in temperatures < -10°C |
| **Mountaineer** | Climb 10,000m cumulative elevation |

---



## 🐛 Troubleshooting

<details>
<summary><strong>No Achievements Showing</strong></summary>

**Symptoms**: All achievements show as ❌ or no data appears

**Solutions**:
1. Verify PostgreSQL datasource connection in Grafana
2. Check that `car_id` matches your actual vehicle ID
3. Ensure you have drives/charges recorded in TeslaMate
4. Validate database permissions for the Grafana user
5. Check datasource UID matches dashboard configuration

```sql
-- Test query to verify data exists
SELECT count(*) FROM drives WHERE car_id = 1;
SELECT count(*) FROM charging_processes WHERE car_id = 1;
```

</details>

<details>
<summary><strong>Incorrect Geofence Calculations</strong></summary>

**Symptoms**: Distance from home achievements don't work correctly

**Solutions**:
1. Verify your home geofence exists in TeslaMate
2. Check geofence name matches search patterns ("Home" or "Casa")
3. Ensure GPS coordinates are accurate in your drives data
4. Update geofence patterns in SQL queries

```sql
-- Check available geofences
SELECT name, latitude, longitude FROM geofences;
```

</details>

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### 🎯 Contribution Areas

- **New Achievement Ideas**: Suggest creative and motivating achievements
- **Bug Reports**: Report issues with detailed descriptions

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Credits

This project builds upon amazing technologies and communities:

- **[TeslaMate](https://github.com/teslamate-org/teslamate)** - Core data logging system
- **[Grafana](https://grafana.com/)** - Powerful visualization platform
- **[PostgreSQL](https://www.postgresql.org/)** - Reliable database backend


Special thanks to the TeslaMate community for creating such a comprehensive data ecosystem.

---


## 💝 Donate & Support

If you find this project useful and want to support its development:

### PayPal Donation
[![Donate with PayPal](https://raw.githubusercontent.com/stefan-niedermann/paypal-donate-button/master/paypal-donate-button.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MUW2XFMQB2782)

### Tesla Referral
Other way to support me is to use my referral link to purchase a Tesla product and get Credits you can redeem for exclusive awards like Supercharging miles, merchandise, and accessories.

<div align="center">
  <img src="https://images.seeklogo.com/logo-png/36/1/tesla-motors-logo-png_seeklogo-365011.png" alt="Tesla Logo" width="100"/>
</div>

**[Use my Tesla referral link](https://ts.la/cristian354389)**

You can see my Tesla gear here: **[teslagear.crstian.me](https://teslagear.crstian.me/)**

Your support helps keep this project maintained and improved! 🙏


---

<div align="center">

**🌟 Star this project if you find it helpful!**

*Made with ❤️ by the Tesla community*

---

**Disclaimer**: This dashboard is for entertainment purposes only. Drive safely and follow all traffic laws. Achievement calculations are estimates and may not reflect all driving conditions.

</div>