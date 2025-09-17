# Requirements Document

## Introduction

This feature adds an AI-powered article summarization capability to Ghost. A "Summarize" button will appear on article pages that allows readers to generate and view an AI summary of the article content. The feature uses OpenRouter's API with the google/gemma-3-27b-it:free model to generate summaries in a secure, production-ready manner that prevents API key exposure and avoids redundant summary generation.

## Requirements

### Requirement 1

**User Story:** As a reader visiting an article page, I want to see a "Summarize" button positioned beneath the article title so that I can quickly generate an AI summary of the article content.

#### Acceptance Criteria

1. WHEN a user visits an article page THEN the system SHALL display a "Summarize" button beneath the article title
2. WHEN the article page loads THEN the system SHALL only show the "Summarize" button on article pages (not on other page types)
3. WHEN the "Summarize" button is displayed THEN it SHALL be positioned between the article title and the article body content

### Requirement 2

**User Story:** As a reader, I want to click the "Summarize" button and see an AI-generated summary appear in a dedicated component so that I can quickly understand the article's key points without affecting the original article layout.

#### Acceptance Criteria

1. WHEN a user clicks the "Summarize" button THEN the system SHALL initiate an AI summary generation request
2. WHEN the AI summary is being generated THEN the system SHALL reveal a summary component that expands and streams the response text in real-time
3. WHEN the summary component is revealed THEN it SHALL be positioned between the "Summarize" button and the article body content
4. WHEN the summary generation is complete THEN the system SHALL display the full summary in the component
5. WHEN the summary generation fails THEN the system SHALL display an appropriate error message in the summary component

### Requirement 3

**User Story:** As a system administrator, I want the OpenRouter API integration to be secure and production-ready with a hardcoded API key so that there is no way for users to input or extract API keys.

#### Acceptance Criteria

1. WHEN the system makes API calls to OpenRouter THEN it SHALL use a hardcoded API key stored securely on the server side
2. WHEN client-side code requests a summary THEN the system SHALL never expose the OpenRouter API key to the browser
3. WHEN API requests are made THEN the system SHALL use the google/gemma-3-27b-it:free model as specified
4. WHEN handling API responses THEN the system SHALL implement proper error handling and rate limiting
5. WHEN the system is deployed THEN there SHALL be no user interface or mechanism for users to input or modify API keys

### Requirement 4

**User Story:** As a reader, I want to avoid waiting for redundant summary generation so that previously generated summaries are displayed immediately in the summary component.

#### Acceptance Criteria

1. WHEN a summary has already been generated for an article THEN the system SHALL display the existing summary in the summary component instead of generating a new one
2. WHEN a user clicks "Summarize" on an article with an existing summary THEN the system SHALL immediately reveal the summary component and display the cached summary
3. WHEN an article is updated THEN the system SHALL invalidate any existing summary to ensure accuracy
4. WHEN storing summaries THEN the system SHALL persist them in a way that survives server restarts

### Requirement 5

**User Story:** As a reader, I want the summary component to be properly sized, scrollable, and responsive so that I can read summaries of any length on both desktop and mobile devices without disrupting the article layout.

#### Acceptance Criteria

1. WHEN the summary component is hidden THEN it SHALL not be visible or take up any space on the page
2. WHEN the summary component is revealed THEN it SHALL expand to display the summary content
3. WHEN the summary component expands THEN it SHALL have a maximum height equivalent to a small paragraph
4. WHEN the summary content exceeds the component's maximum height THEN the component SHALL be scrollable
5. WHEN the summary component is displayed THEN the article body content SHALL remain positioned below it
6. WHEN the summary component is viewed on different screen sizes THEN it SHALL be responsive and maintain proper layout on both desktop and mobile devices

### Requirement 6

**User Story:** As a Ghost site owner, I want the summarization feature to integrate seamlessly with Ghost's existing architecture so that it doesn't disrupt the current functionality.

#### Acceptance Criteria

1. WHEN the feature is installed THEN it SHALL integrate with Ghost's existing theme system
2. WHEN the feature is active THEN it SHALL not interfere with existing article page functionality
3. WHEN the feature processes articles THEN it SHALL work with Ghost's existing content structure and database
4. WHEN users interact with the feature THEN it SHALL maintain Ghost's existing user experience patterns
5. WHEN the feature is active THEN it SHALL never modify the original article content
