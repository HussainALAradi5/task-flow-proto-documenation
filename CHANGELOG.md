# Changelog

All notable changes to TaskFlow Proto will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Added
- Project documentation repository
- Architecture documentation
- API reference documentation
- Roles and permissions documentation

### To Do
- Wire up `restrictTo` middleware on all routes
- Add Zod validation schemas for all endpoints
- Create dedicated signup/login endpoints
- Angular frontend components and routing

## [0.1.0] - 2026-08-12

### Added
- Express.js server with TypeScript
- MongoDB/Mongoose connection (Atlas)
- Base CRUD infrastructure (BaseService, BaseController, BaseRoute)
- 6 domain models: User, Team, Project, Task, Milestone, Event
- TypeScript interfaces for all models
- Enums: GenericStatus, TaskPriority, UserRole, EntityType
- JWT authentication (login, token verification, protect middleware)
- Password hashing with bcrypt
- Role-based authorization middleware (restrictTo)
- User data isolation (admin vs non-admin scoping)
- Auto-role promotion on project creation
- Soft delete pattern (isActive: false)
- Error handling pipeline
- Zod validation utility (exists, not yet applied)
- Event/audit logging model and service
