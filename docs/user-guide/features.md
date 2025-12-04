# Features

GreenMap offers a comprehensive set of features designed to make environmental action easy and impactful. This page details all available features.

## Map Features

### Interactive Mapping

Our core mapping functionality includes:

#### Map Layers

- **Satellite View**: High-resolution satellite imagery
- **Street View**: Detailed street-level mapping
- **Terrain View**: Topographical features
- **Hybrid View**: Combination of satellite and street

#### Map Controls

```javascript
// Example: Basic map interaction
- Pan: Click and drag
- Zoom: Mouse wheel or +/- buttons
- Rotate: Ctrl + drag (3D view)
- Tilt: Right-click + drag
```

#### Custom Markers

Projects are displayed with color-coded markers:

| Color | Project Type | Icon |
|-------|--------------|------|
| 🟢 Green | Tree Planting | 🌳 |
| 🔵 Blue | Water Conservation | 💧 |
| 🟡 Yellow | Cleanup Events | 🗑️ |
| 🟣 Purple | Education | 📚 |
| 🔴 Red | Urgent Action | ⚠️ |

### Location Services

- **Auto-detection**: Automatically find your location
- **Geofencing**: Get notified about nearby projects
- **Route Planning**: Directions to project locations
- **Offline Maps**: Download maps for offline use

## Project Management

### Creating Projects

#### Basic Information

When creating a project, you can specify:

```yaml
Required Fields:
  - Project Name
  - Description
  - Category
  - Location
  - Date & Time

Optional Fields:
  - Cover Image
  - Additional Images
  - Documents/Resources
  - Prerequisites
  - Equipment Needed
  - Target Participants
```

#### Advanced Settings

- **Recurring Events**: Set up repeating projects
- **Team Projects**: Collaborate with other organizers
- **Private Projects**: Invite-only events
- **Prerequisites**: Set requirements for participants
- **Waitlist**: Manage overflow registrations

### Managing Projects

#### Participant Management

- View participant list
- Approve/reject registrations
- Send bulk messages
- Export participant data
- Check-in system for attendance

#### Project Updates

Keep participants informed:

- Send announcements
- Post progress updates
- Share photos and videos
- Update project details
- Cancel or reschedule

#### Impact Tracking

Monitor project outcomes:

**Metrics Available:**
- Number of participants
- Hours contributed
- Resources collected/planted
- Carbon offset achieved
- Area covered
- Before/after photos

## Community Features

### Social Interaction

#### Commenting System

- Comment on projects
- Reply to other comments
- Like/react to comments
- Report inappropriate content
- Tag other users

#### Messaging

- Direct messages to users
- Group chats for teams
- Project-specific discussions
- File sharing
- Voice notes

#### Following System

- Follow other users
- Follow projects
- Activity feed
- Notification preferences

### Achievements & Gamification

#### Badges

Earn badges for various achievements:

| Badge | Requirement | Icon |
|-------|-------------|------|
| First Step | Join your first project | 🎯 |
| Tree Hugger | Plant 10 trees | 🌳 |
| Clean Sweep | Participate in 5 cleanups | 🧹 |
| Eco Warrior | 50+ hours contributed | ⚔️ |
| Community Hero | Organize 10 projects | 🦸 |
| Green Leader | 100+ followers | 👑 |

#### Leaderboards

Compete and inspire:

- Global leaderboard
- Local area rankings
- Category-specific rankings
- Team leaderboards
- Time-based challenges

#### Streaks

Maintain your environmental commitment:

- Daily check-in streaks
- Monthly participation streaks
- Yearly achievement milestones

## User Profile Features

### Profile Customization

Personalize your profile:

- Profile picture and banner
- Bio and description
- Location and interests
- Social media links
- Custom themes

### Impact Dashboard

Your personal environmental impact:

**Statistics Tracked:**
- ✓ Total projects participated
- ✓ Hours volunteered
- ✓ Trees planted
- ✓ Waste collected (kg)
- ✓ CO₂ offset (kg)
- ✓ Water saved (liters)
- ✓ Distance traveled green

### Portfolio

Showcase your work:

- Photo galleries
- Project highlights
- Testimonials
- Certificates
- Media mentions

## Search & Discovery

### Advanced Search

Find exactly what you're looking for:

**Search Filters:**
- Keywords
- Location (radius search)
- Date range
- Category
- Difficulty level
- Duration
- Participant count
- Language

### Recommendations

AI-powered suggestions:

- Projects based on your interests
- Nearby opportunities
- Trending initiatives
- Similar projects
- User recommendations

### Saved Searches

- Save frequent searches
- Get alerts for new matches
- Share searches with others

## Notifications

### Notification Types

Stay informed with timely updates:

| Type | Description | Delivery Method |
|------|-------------|-----------------|
| Project Updates | Changes to joined projects | Email, Push, In-app |
| New Projects | Projects matching interests | Email, Weekly digest |
| Messages | Direct messages from users | Push, Email |
| Achievements | Badges and milestones | In-app, Push |
| Reminders | Upcoming project reminders | Push, Email, SMS |
| Community | Comments, likes, follows | In-app |

### Notification Settings

Customize how you receive notifications:

- Enable/disable by type
- Set quiet hours
- Choose delivery methods
- Frequency preferences

## Mobile App Features

### Mobile-Specific

Features exclusive to mobile:

- **QR Code Check-in**: Quick event registration
- **Offline Mode**: Access saved content offline
- **Camera Integration**: Instant photo uploads
- **Push Notifications**: Real-time alerts
- **Location Services**: Auto-discovery of nearby projects
- **Calendar Integration**: Sync with device calendar

## Reporting & Analytics

### Personal Reports

Generate reports on your impact:

- Monthly summary reports
- Annual impact statements
- Custom date range reports
- Exportable data (CSV, PDF)

### Project Reports

For organizers:

- Participation statistics
- Demographics breakdown
- Impact metrics
- Feedback analysis
- Photo collages

## Integration Features

### Calendar Integration

Sync with your favorite calendar:

- Google Calendar
- Apple Calendar
- Outlook Calendar
- Custom ICS export

### Social Media

Share your impact:

- One-click sharing
- Custom share templates
- Auto-posting (optional)
- Social media previews

### Third-Party Apps

Connect with other platforms:

- Strava (track green commutes)
- Fitbit (track activity)
- iNaturalist (biodiversity)
- Weather apps (event planning)

## Accessibility Features

Ensuring everyone can participate:

- **Screen Reader Support**: Full ARIA compliance
- **Keyboard Navigation**: Complete keyboard control
- **High Contrast Mode**: Enhanced visibility
- **Text Scaling**: Adjustable font sizes
- **Voice Commands**: Hands-free operation
- **Closed Captions**: Video accessibility
- **Multiple Languages**: 15+ languages supported

## Privacy & Security

### Privacy Controls

- **Profile Visibility**: Public, friends, or private
- **Location Sharing**: Control who sees your location
- **Activity Visibility**: Hide specific activities
- **Data Download**: Export all your data
- **Account Deletion**: Full data removal

### Security Features

- Two-factor authentication (2FA)
- Login alerts
- Session management
- Encrypted communications
- Regular security audits

## FAQ

### General Questions

**Q: Is GreenMap free to use?**  
A: Yes! Basic features are completely free. Premium features are available for organizers and organizations.

**Q: Can I use GreenMap offline?**  
A: Yes, you can download maps and project information for offline viewing in the mobile app.

**Q: How is impact calculated?**  
A: Impact metrics are calculated based on established environmental standards and verified data from project organizers.

**Q: Can I create private projects?**  
A: Yes, you can create private, invite-only projects with an Organizer account.

**Q: Is my data secure?**  
A: Absolutely. We use industry-standard encryption and never sell your personal data.

### Technical Questions

**Q: Which browsers are supported?**  
A: Chrome, Firefox, Safari, and Edge (latest versions).

**Q: Is there an API?**  
A: Yes! Check our [API Reference](../api-reference/overview.md) for details.

**Q: Can I export my data?**  
A: Yes, you can export all your data from Settings → Privacy → Download Data.

---

*Explore all these features and start making an impact today!*
