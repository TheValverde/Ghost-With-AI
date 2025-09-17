# Implementation Plan

- [ ] 1. Create database migration for post summaries table
  - Create migration file following Ghost's naming convention (YYYY-MM-DD-HH-MM-SS-description.js)
  - Define post_summaries table schema with proper foreign key relationships
  - Include up and down migration functions
  - _Requirements: 4.1, 4.2, 4.3, 4.4_

- [ ] 2. Implement PostSummary model
  - Create PostSummary model extending Ghost's base model
  - Define table relationships with Post model
  - Implement model methods for finding summaries by post ID
  - Add model to Ghost's model index
  - _Requirements: 4.1, 4.2, 4.3, 4.4_

- [ ] 3. Create OpenRouter service for AI integration
  - Implement service class for OpenRouter API communication
  - Add hardcoded API key configuration (server-side only)
  - Implement streaming response handling for real-time generation
  - Add simulated streaming for cached responses with artificial delay
  - Include error handling and retry logic
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5_

- [ ] 4. Implement post summary API endpoint
  - Create post-summaries.js endpoint following Ghost's API pattern
  - Implement read method for getting/generating summaries
  - Add streaming response functionality for both cached and new summaries
  - Integrate with Ghost's caching system
  - Include proper error handling and validation
  - _Requirements: 2.1, 2.2, 2.4, 2.5, 3.1, 3.2, 3.3, 3.4, 4.1, 4.2_

- [ ] 5. Register API endpoint in Ghost's routing system
  - Add post-summaries endpoint to API endpoints index
  - Configure routing for /api/content/posts/:id/summary
  - Ensure public access (no authentication required)
  - _Requirements: 1.1, 1.2, 1.3, 2.1_

- [ ] 6. Create frontend summary component JavaScript
  - Implement JavaScript module for summary component functionality
  - Add button click handling to reveal summary component
  - Implement streaming text display with character-by-character animation
  - Add API request handling with proper error states
  - Include responsive behavior for mobile and desktop
  - _Requirements: 1.1, 1.3, 2.1, 2.2, 2.3, 2.5, 5.1, 5.2, 5.4, 5.6_

- [ ] 7. Create Handlebars helper for summary component
  - Implement article_summary helper following Ghost's helper pattern
  - Generate HTML structure for summary button and container
  - Ensure component is hidden by default
  - Include proper ARIA labels for accessibility
  - _Requirements: 1.1, 1.3, 5.1, 5.2, 5.5_

- [ ] 8. Add CSS styles for summary component
  - Create responsive styles for summary button and container
  - Implement smooth reveal/hide animations
  - Add scrollable content area with proper max-height
  - Ensure consistent styling with Ghost's design system
  - Include mobile-responsive breakpoints
  - _Requirements: 5.1, 5.2, 5.3, 5.4, 5.5, 5.6_

- [ ] 9. Integrate summary component into article templates
  - Modify Ghost's default article template to include summary helper
  - Position component between article title and body content
  - Ensure integration works with existing theme system
  - Test with different Ghost themes
  - _Requirements: 1.1, 1.3, 6.1, 6.2, 6.3, 6.4_

- [ ] 10. Implement cache invalidation logic
  - Add logic to invalidate summaries when posts are updated
  - Integrate with Ghost's existing post update hooks
  - Ensure summary regeneration triggers when article content changes
  - _Requirements: 4.3, 6.3_

- [ ] 11. Add comprehensive error handling
  - Implement frontend error states for network failures
  - Add backend error handling for API failures
  - Create user-friendly error messages
  - Add fallback behavior when service is unavailable
  - _Requirements: 2.4, 3.4_

- [ ] 12. Create unit tests for PostSummary model
  - Write tests for model CRUD operations
  - Test relationship with Post model
  - Validate data integrity and constraints
  - Test findByPostId method functionality
  - _Requirements: 4.1, 4.2, 4.3, 4.4_

- [ ] 13. Create unit tests for OpenRouter service
  - Test API communication with mocked responses
  - Validate streaming functionality for both real and simulated responses
  - Test error handling and retry logic
  - Verify API key security (never exposed)
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5_

- [ ] 14. Create integration tests for summary API endpoint
  - Test complete summary generation workflow
  - Validate streaming response format
  - Test caching behavior and cache invalidation
  - Test error scenarios and proper HTTP status codes
  - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5, 4.1, 4.2, 4.3_

- [ ] 15. Create frontend component tests
  - Test button click interactions and component reveal
  - Validate streaming text display functionality
  - Test responsive behavior across different screen sizes
  - Test error state handling and user feedback
  - _Requirements: 1.1, 1.3, 2.1, 2.2, 2.3, 5.1, 5.2, 5.4, 5.6_

- [ ] 16. Perform end-to-end testing
  - Test complete user workflow from button click to summary display
  - Validate behavior with both cached and new summaries
  - Test across different browsers and devices
  - Verify accessibility compliance
  - _Requirements: 1.1, 1.2, 1.3, 2.1, 2.2, 2.3, 2.4, 2.5, 5.6, 6.4_
