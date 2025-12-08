<div align="center">
  <img src="https://cdn.crstian.me/teslamate-achievements-logo.png" alt="TeslaMate Achievements" width="200"/>




# TeslaMate Achievements Dashboard 🏆

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Grafana](https://img.shields.io/badge/Grafana-12.1.1+-orange?style=for-the-badge&logo=grafana)](https://grafana.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16+-blue?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)
[![TeslaMate](https://img.shields.io/badge/TeslaMate-Compatible-green?style=for-the-badge)](https://github.com/teslamate-org/teslamate)

*A comprehensive gamification dashboard for TeslaMate that tracks and displays various driving achievements based on your Tesla vehicle data.*

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

### 🎯 Perfect for

- **Tesla Enthusiasts** who want to gamify their driving experience
- **Data-driven Drivers** who love tracking metrics and progress
- **Eco-conscious Owners** monitoring their environmental impact
- **Long-distance Travelers** documenting their journeys
- **Daily Commuters** optimizing their efficiency and habits

---

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have:

- ✅ **TeslaMate**: Fully functional instance with PostgreSQL database
- ✅ **Grafana**: Version 12.1.1 or higher with table panel support
- ✅ **PostgreSQL**: Direct access to your TeslaMate database
- ✅ **Basic SQL Knowledge**: For customization and troubleshooting

### Installation

1. **Download the Dashboard**
   ```bash
   # Clone this repository
   git clone https://github.com/your-username/teslamate-achievements.git
   cd teslamate-achievements

   # Or download the JSON directly
   wget https://raw.githubusercontent.com/your-username/teslamate-achievements/main/achivements-dashboard.json
   ```

2. **Import to Grafana**
   - Open your Grafana instance
   - Navigate to **Dashboards** → **Import**
   - Upload the `achivements-dashboard.json` file
   - Configure the PostgreSQL datasource connection
   - Verify the datasource UID (default: `PC98BA2F4D77E1A42`)

3. **Configure Car Settings**
   ```sql
   -- Edit the dashboard queries to match your car ID
   WHERE car_id = 1  -- Replace with your actual car ID
   ```

4. **Verify Installation**
   - Check that achievements display correctly
   - Validate data connections
   - Test dashboard functionality

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

## 📊 Dashboard Features

### Visual Design

- **Status Indicators**: 🏆 for completed, ❌ for locked achievements
- **Color Coding**: Green for achievements, red for incomplete
- **Category Organization**: Logical grouping of related achievements
- **Progress Tracking**: Real-time updates as you drive

### Data Processing

- **Real-time Calculations**: Achievement status updates immediately
- **SQL Optimization**: Efficient queries for fast dashboard loading
- **Historical Analysis**: Uses all available TeslaMate data
- **Cross-referenced Data**: Combines drives, charges, positions, and geofences

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
- **SQL Optimization**: Improve query performance and accuracy
- **Documentation**: Enhance README and add examples
- **Bug Reports**: Report issues with detailed descriptions
- **Feature Requests**: Propose new functionality

### 📝 Development Guidelines

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/amazing-achievement`
3. **Make** your changes with proper documentation
4. **Test** thoroughly with different datasets
5. **Submit** a pull request with clear description

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

## 📞 Support

### Getting Help

If you encounter issues or have questions:

1. **Check Troubleshooting**: Review the [troubleshooting section](#-troubleshooting) above
2. **Search Issues**: Check existing [GitHub issues](https://github.com/your-username/teslamate-achievements/issues)
3. **Verify TeslaMate**: Ensure your TeslaMate setup is working correctly
4. **Community Support**: Ask in TeslaMate community forums

### Issue Reporting

When reporting issues, please include:

- ✅ **Grafana Version**: Your Grafana instance version
- ✅ **TeslaMate Version**: Your TeslaMate setup details
- ✅ **Database Schema**: PostgreSQL version and any customizations
- ✅ **Error Messages**: Complete error messages and logs
- ✅ **Steps to Reproduce**: Detailed reproduction steps
- ✅ **Expected vs Actual**: What you expected vs what happened

---

<div align="center">

**🌟 Star this project if you find it helpful!**

*Made with ❤️ by the Tesla community*

---

**Disclaimer**: This dashboard is for entertainment purposes only. Drive safely and follow all traffic laws. Achievement calculations are estimates and may not reflect all driving conditions.

</div>