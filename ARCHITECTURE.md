# Morpheus Phase 1

## Foundation

Morpheus is organized around durable knowledge objects and first-class relations. The browser experience uses the authenticated Supabase workspace API when environment variables and a signed-in session are present, and falls back to local browser persistence when they are absent. The persisted model maps directly to the Supabase migration in `supabase/migrations/001_initial_schema.sql`.

## Phase 1 routes

- `/` - data-driven workspace dashboard, search, capture, and object browser
- `/commands` - reserved route for the Command Vault view
- `/projects` - reserved route for project knowledge
- `/troubleshooting` - reserved route for procedure and problem flows
- `/settings` - reserved route for authentication and workspace settings

The initial UI keeps these as workspace modes so the core object model is visible immediately. They can become dedicated routes without changing the data contracts.

## Core model

- `knowledge_objects`: shared object identity and content across concepts, commands, projects, procedures, and future types
- `categories`: user-owned, optionally nested classification
- `tags` and `knowledge_tags`: normalized labels
- `knowledge_relations`: directed, typed graph edges
- `activity_events`: append-only history for future recommendations, review scheduling, and analytics

Knowledge state is an explicit field rather than a visual decoration. Confidence is a bounded numeric signal that can later be updated by review, quiz, lab, and project events.

## Security

Supabase policies scope every row to `auth.uid()`. Client credentials belong only in environment variables, and the public anon key is safe to expose only alongside correct RLS policies. User content should be rendered as untrusted Markdown in a later editor implementation with sanitization.

## Next phases

1. Add a repository interface around the existing workspace API and migrate relation/tag writes through it.
2. Add relation management, backlinks, and activity timeline queries.
3. Add quizzes, labs, review scheduling, and learning paths.
4. Add embeddings and relationship-aware retrieval only after the relational foundation is in use.
