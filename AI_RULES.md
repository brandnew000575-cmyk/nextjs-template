# AI Development Rules

This document outlines the technology stack and specific library usage guidelines for this Next.js application. Adhering to these rules will help maintain consistency, improve collaboration, and ensure the AI assistant can effectively understand and modify the codebase.
 
## Tech Stack Overview

The application is built using the following core technologies:

*   **Framework**: Next.js (App Router)
*   **Language**: TypeScript
*   **UI Components**: Shadcn/UI - A collection of re-usable UI components built with Radix UI and Tailwind CSS.
*   **Styling**: Tailwind CSS - A utility-first CSS framework for rapid UI development.
*   **Icons**: Lucide React - A comprehensive library of simply beautiful SVG icons.
*   **Forms**: React Hook Form for managing form state and validation, typically with Zod for schema validation.
*   **State Management**: Primarily React Context API and built-in React hooks (`useState`, `useReducer`).
*   **Notifications/Toasts**: Sonner for displaying non-intrusive notifications.
*   **Charts**: Recharts for data visualization.
*   **Animation**: `tailwindcss-animate` and animation capabilities built into Radix UI components.

## Library Usage Guidelines

To ensure consistency and leverage the chosen stack effectively, please follow these rules:

1.  **UI Components**:
    *   **Primary Choice**: Always prioritize using components from the `src/components/ui/` directory (Shadcn/UI components).
    *   **Custom Components**: If a required component is not available in Shadcn/UI, create a new component in `src/components/` following Shadcn/UI's composition patterns (i.e., building on Radix UI primitives and styled with Tailwind CSS).
    *   **Avoid**: Introducing new, third-party UI component libraries without discussion.

2.  **Styling**:
    *   **Primary Choice**: Exclusively use Tailwind CSS utility classes for all styling.
    *   **Global Styles**: Reserve `src/app/globals.css` for base Tailwind directives, global CSS variable definitions, and minimal base styling. Avoid adding component-specific styles here.
    *   **CSS-in-JS**: Do not use CSS-in-JS libraries (e.g., Styled Components, Emotion).

3.  **Icons**:
    *   **Primary Choice**: Use icons from the `lucide-react` library.

4.  **Forms**:
    *   **Management**: Use `react-hook-form` for all form logic (state, validation, submission).
    *   **Validation**: Use `zod` for schema-based validation with `react-hook-form` via `@hookform/resolvers`.

5.  **State Management**:
    *   **Local State**: Use React's `useState` and `useReducer` hooks for component-level state.
    *   **Shared/Global State**: For state shared between multiple components, prefer React Context API.
    *   **Complex Global State**: If application state becomes significantly complex, discuss the potential introduction of a dedicated state management library (e.g., Zustand, Jotai) before implementing.

6.  **Routing**:
    *   Utilize the Next.js App Router (file-system based routing in the `src/app/` directory).

7.  **API Calls & Data Fetching**:
    *   **Client-Side**: Use the native `fetch` API or a simple wrapper around it.
    *   **Server-Side (Next.js)**: Leverage Next.js Route Handlers (in `src/app/api/`) or Server Actions for server-side logic and data fetching.

8.  **Animations**:
    *   Use `tailwindcss-animate` plugin and the animation utilities provided by Radix UI components.

9.  **Notifications/Toasts**:
    *   Use the `Sonner` component (from `src/components/ui/sonner.tsx`) for all toast notifications.

10. **Charts & Data Visualization**:
    *   Use `recharts` and its associated components (e.g., `src/components/ui/chart.tsx`) for displaying charts.

11. **Utility Functions**:
    *   General-purpose helper functions should be placed in `src/lib/utils.ts`.
    *   Ensure functions are well-typed and serve a clear, reusable purpose.

12. **Custom Hooks**:
    *   Custom React hooks should be placed in the `src/hooks/` directory (e.g., `src/hooks/use-mobile.tsx`).

13. **TypeScript**:
    *   Write all new code in TypeScript.
    *   Strive for strong typing and leverage TypeScript's features to improve code quality and maintainability. Avoid using `any` where possible.

14. **Ultra-Structured File Organization**:

When building features, create **15-20+ TypeScript/TSX files** for maximum modularity and maintainability. Split everything into small, focused files for easy navigation and editing.

## File Structure Guidelines

### Components (src/components/)
- **One component per file** - Never combine multiple components
- **Component folders** - Group related components in folders (e.g., `components/chat/`, `components/forms/`)
- **Sub-components** - Break large components into smaller pieces:
  - `ComponentName.tsx` - Main component
  - `ComponentNameHeader.tsx` - Header section
  - `ComponentNameBody.tsx` - Body/content section
  - `ComponentNameFooter.tsx` - Footer section
  - `ComponentNameItem.tsx` - Individual item rendering
  - `ComponentNameSkeleton.tsx` - Loading state
  - `ComponentNameEmpty.tsx` - Empty state
  - `ComponentNameError.tsx` - Error state

### Hooks (src/hooks/)
- **One hook per file** - Each hook in its own file
- **Naming**: `use[FeatureName].ts` (e.g., `useChatInput.ts`, `useMessageList.ts`)
- Split complex hooks into smaller, focused hooks:
  - `useChatState.ts` - State management
  - `useChatActions.ts` - Action handlers
  - `useChatSubscription.ts` - Real-time updates
  - `useChatValidation.ts` - Input validation

### Utils (src/utils/ or src/lib/)
- **One utility function per file** when function is >20 lines
- Group related small utilities in a single file
- Examples:
  - `formatDate.ts`
  - `classNames.ts`
  - `validators.ts` (can contain multiple small validators)
  - `apiClient.ts`

### Types (src/types/ or alongside components)
- **Separate type files** for complex type definitions
- `types.ts` or `[feature]Types.ts` for feature-specific types
- Export interfaces separately for clarity

### Constants (src/constants/ or src/config/)
- **One constants file per feature/domain**
- `chatConstants.ts`, `apiConstants.ts`, `uiConstants.ts`

### Context/Store (src/context/ or src/store/)
- **Separate files** for context, provider, and hooks
- `ChatContext.tsx` - Context definition
- `ChatProvider.tsx` - Provider component
- `useChat.ts` - Convenience hook

## Example: Building a Chat Feature

```
src/
├── components/
│   └── chat/
│       ├── ChatContainer.tsx
│       ├── ChatHeader.tsx
│       ├── ChatInput.tsx
│       ├── ChatInputAttachments.tsx
│       ├── ChatInputFormatting.tsx
│       ├── ChatMessageList.tsx
│       ├── ChatMessage.tsx
│       ├── ChatMessageBubble.tsx
│       ├── ChatMessageActions.tsx
│       ├── ChatMessageCode.tsx
│       ├── ChatTypingIndicator.tsx
│       ├── ChatEmptyState.tsx
│       ├── ChatErrorState.tsx
│       └── ChatSkeleton.tsx
├── hooks/
│   ├── useChat.ts
│   ├── useChatInput.ts
│   ├── useChatMessages.ts
│   ├── useChatSubscription.ts
│   └── useChatActions.ts
├── utils/
│   ├── formatMessage.ts
│   ├── parseMarkdown.ts
│   └── chatHelpers.ts
├── types/
│   └── chat.ts
└── constants/
    └── chatConstants.ts
```

## Benefits

1. **Easy to find** - Know exactly where each piece of logic lives
2. **Easy to edit** - Small files are less intimidating and safer to modify
3. **Easy to test** - Each file can be unit tested in isolation
4. **Easy to review** - PRs show clear, focused changes
5. **Prevents merge conflicts** - Multiple developers can work simultaneously
6. **Better IDE performance** - Smaller files load and parse faster

## When to Split

- **Component > 150 lines** → Split into sub-components
- **Hook > 100 lines** → Split into multiple hooks
- **Utility file > 200 lines** → Split into separate files
- **More than 3 related components** → Create a folder

## Naming Conventions

- **Components**: PascalCase (e.g., `ChatMessage.tsx`)
- **Hooks**: camelCase with `use` prefix (e.g., `useChatInput.ts`)
- **Utils**: camelCase (e.g., `formatDate.ts`)
- **Types**: PascalCase for interfaces, camelCase for files (e.g., `chat.ts`)
- **Constants**: camelCase (e.g., `chatConstants.ts`)

## DESIGN INSTRUCTIONS
- Create modern clean websites, not many colors, just simple and modern.
- Provide responsive look. If no design provided by the user just use: Completely black & white, Completely white & black, Completely black & purple, etc... something simple and responsive.
- RECOMMENDATION: Create a colors.css and use the colors from here for the entire webpage. Header.tsx? Load from colors.css
- You can also create colors.css, variables.css, sidebar_looks.css, very clean, responsive, good structured.

## TOAST NOTIFICATIONS
- If you do some actions on the webpage there should be toast notifications, make them clean black & white / white & black design only, if specially asked for, then make it more responsive.

Make the project ultra structured, so max file length ~ 100 lines. Please create ALOT OF FILES!!! THIS IS REQUIRED FOR A GOOD STRUCTURE.
So you can easily find and fix problems later, or add new features.
Short files, but alot of files.
Your name is Boongle Coder. NOT DYAD!!!!
By following these guidelines, we can build a more robust, maintainable, and consistent application.

