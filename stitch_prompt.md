# Prompt for Reclaim Website Wireframe (Stitch)

## Overview
**Project Name:** Reclaim
**Purpose:** A community-driven platform for reporting and finding lost items.
**Target Audience:** General public, students, commuters.
**Core Functionality:** Users browse listings of lost/found items, filter by category/location, and post new reports.

---

## Visual Style & Theme
*   **Typography:** Modern Sans-Serif (Plus Jakarta Sans).
*   **Primary Color:** Reliable Blue (`#2563EB` / `blue-600`).
*   **Secondary Colors:** 
    *   Lost Items: Red (`#DC2626` / `red-600`).
    *   Found Items: Green (`#16A34A` / `green-600`).
*   **Backgrounds:** Clean white (`#FFFFFF`) / Light Gray (`#F9FAFB`) for cards.
*   **Dark Mode:** Supported (Dark Gray/Black backgrounds), but wireframe can focus on light mode structure.
*   **Iconography:** Simple, clean outline icons (Lucide React style).

---

## Layout Structure

### 1. Navbar (Sticky Top)
*   **Container**: Full width, white background, bottom border.
*   **Left**: 
    *   **Logo**: Icon + "Reclaim" text (Bold, Blue).
*   **Center**: 
    *   **Search Bar** (Desktop): Rounded input "Search for items..." with search icon.
    *   **Nav Pills**: "Browse", "Dashboard", "Messages" (if logged in). Active state has a pill background.
*   **Right**:
    *   **Theme Toggle**: Sun/Moon icon.
    *   **Auth State (Logged Out)**: "Login" (Ghost Button) and "Register" (Primary Button).
    *   **Auth State (Logged In)**: User Profile Dropdown (Avatar + Name).

### 2. Main Content Area (Home Page)
The page has a max-width container (e.g., `max-w-7xl`).

#### A. Hero Section (Conditional - Logged Out Only)
*   **Style**: Light Blue background panel (`bg-blue-50`), rounded corners.
*   **Content**: 
    *   Headline: "Lost & Found Community".
    *   Subtext: "Find what you lost. Return what you found."
    *   CTA Button: "+ Report an Item" (Large, Primary).

#### B. Main Grid Layout
A 2-column layout on Desktop: Sidebar (Left, 25%) and Content (Right, 75%).

**Left Sidebar (Filters)**
*   **Header**: "Filters" title + "Clear all" link.
*   **Status Section**: Checkboxes for "Lost Item" and "Found Item".
*   **Category Section**: Checkboxes for categories (Electronics, Accessories, Documents, Clothing, Keys, Other).
*   **Location Section**:
    *   **Dropdowns**: Country, State, City (dependent selects).
    *   **Specific Address**: Text input "e.g. Eiffel Tower" with a "Go" button.

**Right Content (Item Grid)**
*   **Grid**: 3 columns of cards on large screens, 2 on medium, 1 on mobile.
*   **Item Card Component**:
    *   **Header**: User Avatar + Name (small) + Date (right aligned) + Status Badge (Lost/Found pill).
    *   **Image**: Large square aspect ratio (`aspect-square`) image area. Fallback to gray placeholder if no image.
    *   **Content**:
        *   Title: Bold, truncated (1 line).
        *   Location Badge: Icon + Text (City/Address).
    *   **Footer**:
        *   Category Badge: Pill style.
    *   **Interactions**: Hover splits scale slightly, shadow increases.

#### C. Mobile Specifics
*   **Search**: Full-width search bar below navbar.
*   **Filter Trigger**: "Filters" button with icon (opens Modal/Drawer).
*   **Menu**: Hamburger menu icon in Navbar (opens slide-out drawer with profile & nav links).

### 3. Footer
*   **Container**: White background, top border.
*   **Columns**:
    1.  **Brand**: Logo + Short description text.
    2.  **Quick Links**: Browse Items, Report Item, Dashboard.
    3.  **Contact**: Email (`support.reclaim@gmail.com`), Location (`Mumbai, Maharashtra`).
*   **Bottom**: Copyright text centered.

---

## Detailed Component Specifications

### Item Card
*   **Border**: Thin gray border (`border-gray-200`).
*   **Shadow**: None by default, shadow-md on hover.
*   **Radius**: Rounded-lg or xl.
*   **Status Badge Colors**:
    *   **Lost**: Red background (`bg-red-100`), Red text (`text-red-800`).
    *   **Found**: Green background (`bg-green-100`), Green text (`text-green-800`).

### Filter Sidebar
*   **Position**: Sticky (`top-20`) so it stays visible while scrolling results.
*   **Spacing**: Vertical rhythm between sections (`space-y-8`).

### Buttons
*   **Primary**: Blue background, white text, rounded-md.
*   **Ghost**: Transparent background, hover gray.
*   **Outline**: White background, border gray/blue.

---

## Dashboard View (Optional Secondary Screen)
If generating the Dashboard instead of Home:

### Layout
*   **Header**: "My Dashboard" (H1) + "Post New Item" (Button) on the right.
*   **Sections**:
    1.  **My Reports**: List of items user posted. Uses `DashboardItemCard` (similar to ItemCard but with Edit/Delete actions).
    2.  **My Retrievals** (Items I Found): List of claims user made on lost items. Uses `ClaimCard`.
    3.  **My Claims** (Items I Lost): List of claims made on user's found items. Uses `ClaimCard`.
*   **Empty States**: Dashed border box with icon + text "No items yet".
