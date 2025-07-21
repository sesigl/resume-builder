# Resume Builder CLI Specification

## Overview

A TypeScript-based CLI tool that generates tailored, professional resumes using LaTeX templating and AI-powered content optimization. Uses human-readable JSON files for data storage, making it easy to edit and version control. Designed for individual job seekers who want to create position-specific resumes while maintaining a centralized repository of their professional information.

## Target User

Individual job seekers comfortable with command-line tools and basic file editing (JSON), who apply to multiple positions and need tailored resumes for each application.

## Core Architecture

### Project Structure
```
resume-builder/
├── personal/                     # Shared personal data (version controlled)
│   ├── contact.json             # Name, email, phone, LinkedIn, etc.
│   ├── skills.json              # Technical & soft skills with examples
│   ├── experience.json          # Complete work history
│   └── education.json           # Education, certifications, awards
├── applications/                # Position-specific applications
│   ├── 2024-01-15-tech-lead-google/
│   │   ├── job-description.txt  # Original job posting
│   │   ├── job-analysis.json    # AI-extracted requirements
│   │   ├── resume-config.json   # Application-specific overrides
│   │   ├── resume.pdf           # Generated resume
│   │   └── resume.tex           # Generated LaTeX source
│   └── 2024-01-20-senior-dev-meta/
│       └── ...
├── templates/                   # LaTeX templates
│   └── professional.tex        # Single, polished professional template
└── config.json                # Global CLI configuration
```

## Data Schema (JSON Files)

### personal/contact.json
```json
{
  "name": "John Doe",
  "email": "john.doe@email.com",
  "phone": "+1-555-123-4567",
  "location": "San Francisco, CA",
  "linkedin": "linkedin.com/in/johndoe",
  "github": "github.com/johndoe",
  "website": "johndoe.dev",
  "updated_at": "2024-01-15T10:30:00Z"
}
```

### personal/skills.json
```json
{
  "technical": [
    {
      "id": "js-ts",
      "name": "JavaScript/TypeScript",
      "proficiency": "expert",
      "years": 5,
      "category": "programming",
      "keywords": ["javascript", "typescript", "js", "ts", "react", "node"],
      "examples": [
        {
          "text": "Built scalable React applications serving 100K+ users",
          "metrics": "100K+ users",
          "context": "project"
        },
        {
          "text": "Migrated legacy codebase to TypeScript, reducing bugs by 40%",
          "metrics": "40% bug reduction",
          "context": "achievement"
        }
      ],
      "is_active": true
    },
    {
      "id": "nodejs",
      "name": "Node.js",
      "proficiency": "advanced",
      "years": 4,
      "category": "backend",
      "keywords": ["node", "nodejs", "express", "api", "backend"],
      "examples": [
        {
          "text": "Designed microservices architecture handling 10M+ requests/day",
          "metrics": "10M+ requests/day",
          "context": "architecture"
        }
      ],
      "is_active": true
    }
  ],
  "soft_skills": [
    {
      "id": "leadership",
      "name": "Leadership",
      "keywords": ["leadership", "management", "team", "mentor"],
      "examples": [
        {
          "text": "Led cross-functional team of 8 engineers on major product launch",
          "metrics": "8 engineers",
          "context": "leadership"
        },
        {
          "text": "Mentored 3 junior developers, all promoted within 18 months",
          "metrics": "3 promotions in 18 months",
          "context": "mentoring"
        }
      ],
      "is_active": true
    }
  ],
  "updated_at": "2024-01-15T10:30:00Z"
}
```

### personal/experience.json
```json
{
  "positions": [
    {
      "id": "techcorp-senior",
      "company": "TechCorp Inc.",
      "title": "Senior Software Engineer",
      "start_date": "2022-01",
      "end_date": null,
      "location": "San Francisco, CA",
      "employment_type": "full-time",
      "industry": "fintech",
      "company_size": "medium",
      "is_current": true,
      "technologies": ["React", "Node.js", "PostgreSQL", "AWS", "Docker"],
      "achievements": [
        {
          "id": "engagement-increase",
          "title": "Increased user engagement by 35%",
          "description": "Redesigned user onboarding flow using React and data analytics",
          "impact_metric": "35% increase",
          "affected_scope": "50K+ users",
          "achievement_type": "performance",
          "technologies_used": ["React", "Analytics", "A/B Testing"],
          "keywords": ["user experience", "engagement", "onboarding", "react"]
        },
        {
          "id": "deployment-optimization",
          "title": "Reduced deployment time by 80%",
          "description": "Implemented CI/CD pipeline with Docker and GitHub Actions",
          "impact_metric": "80% reduction",
          "time_saved": "From 2 hours to 20 minutes per deployment",
          "achievement_type": "process",
          "technologies_used": ["Docker", "GitHub Actions", "CI/CD"],
          "keywords": ["devops", "automation", "deployment", "docker"]
        }
      ],
      "responsibilities": [
        "Led development of core payment processing features",
        "Collaborated with product team on feature specifications",
        "Code review and mentoring of junior developers",
        "Architected scalable microservices for high-traffic applications"
      ]
    },
    {
      "id": "startup-engineer",
      "company": "StartupCo",
      "title": "Software Engineer",
      "start_date": "2020-06",
      "end_date": "2021-12",
      "location": "San Francisco, CA",
      "employment_type": "full-time",
      "industry": "edtech",
      "company_size": "startup",
      "is_current": false,
      "technologies": ["Python", "Django", "PostgreSQL", "AWS"],
      "achievements": [
        {
          "id": "platform-launch",
          "title": "Launched educational platform from scratch",
          "description": "Built full-stack application serving 5K+ students",
          "impact_metric": "5K+ active users",
          "achievement_type": "innovation",
          "technologies_used": ["Python", "Django", "React"],
          "keywords": ["full-stack", "education", "platform", "launch"]
        }
      ],
      "responsibilities": [
        "Developed full-stack web applications using Python and React",
        "Implemented user authentication and payment processing",
        "Collaborated with designers on user interface improvements"
      ]
    }
  ],
  "updated_at": "2024-01-15T10:30:00Z"
}
```

### personal/education.json
```json
{
  "degrees": [
    {
      "id": "cs-masters",
      "institution": "Stanford University",
      "degree": "Master of Science",
      "field": "Computer Science",
      "start_date": "2018-09",
      "end_date": "2020-06",
      "gpa": "3.8",
      "relevant_coursework": [
        "Machine Learning",
        "Distributed Systems",
        "Software Engineering"
      ],
      "thesis": {
        "title": "Scalable Machine Learning for Real-time Applications",
        "advisor": "Dr. Jane Smith"
      }
    }
  ],
  "certifications": [
    {
      "id": "aws-solutions",
      "name": "AWS Certified Solutions Architect",
      "issuer": "Amazon Web Services",
      "date_earned": "2023-03",
      "expiration_date": "2026-03",
      "credential_id": "AWS-123456789"
    }
  ],
  "updated_at": "2024-01-15T10:30:00Z"
}
```

### Application-specific Files

#### applications/{app-id}/job-analysis.json
```json
{
  "job_info": {
    "company": "Google",
    "position": "Tech Lead",
    "application_date": "2024-01-15",
    "application_deadline": "2024-02-01",
    "job_url": "https://careers.google.com/jobs/tech-lead-123"
  },
  "extracted_requirements": {
    "must_have": [
      {
        "text": "5+ years of software engineering experience",
        "category": "experience",
        "matched_experiences": ["techcorp-senior", "startup-engineer"],
        "confidence": 0.95
      },
      {
        "text": "Proficiency in JavaScript and modern frameworks",
        "category": "technical",
        "matched_skills": ["js-ts"],
        "confidence": 0.90
      }
    ],
    "preferred": [
      {
        "text": "Experience with microservices architecture",
        "category": "technical",
        "matched_achievements": ["deployment-optimization"],
        "confidence": 0.85
      }
    ]
  },
  "keywords": [
    "leadership", "javascript", "react", "microservices", 
    "scalability", "team management", "technical vision"
  ],
  "company_culture": [
    "innovation", "collaboration", "impact", "growth mindset"
  ],
  "ai_analysis": {
    "role_seniority": "senior",
    "technical_focus": ["frontend", "architecture", "leadership"],
    "team_size": "large",
    "impact_scope": "high"
  },
  "generated_at": "2024-01-15T11:00:00Z"
}
```

#### applications/{app-id}/resume-config.json
```json
{
  "generation_settings": {
    "selected_skills": ["js-ts", "nodejs", "leadership"],
    "selected_experiences": ["techcorp-senior", "startup-engineer"],
    "skill_ordering": "relevance",
    "experience_ordering": "reverse_chronological",
    "max_achievements_per_role": 3,
    "include_education": true,
    "include_certifications": true
  },
  "customizations": {
    "summary_focus": "technical leadership and scalability",
    "skill_emphasis": ["JavaScript", "Team Leadership", "System Architecture"],
    "excluded_content": [],
    "custom_sections": []
  },
  "ai_generated_content": {
    "summary": "Experienced Senior Software Engineer with 5+ years building scalable web applications and leading cross-functional teams. Proven track record of improving system performance by 80% and user engagement by 35% through innovative technical solutions and strong leadership. Expertise in JavaScript/TypeScript, React, and microservices architecture with experience managing teams of 8+ engineers.",
    "tailored_achievements": [
      {
        "original_id": "engagement-increase",
        "tailored_text": "Led user experience optimization initiative using React and data analytics, resulting in 35% increase in user engagement across 50K+ active users"
      }
    ]
  },
  "validation_results": {
    "completeness_score": 0.95,
    "relevance_score": 0.88,
    "requirements_coverage": 0.92,
    "missing_elements": [],
    "suggestions": [
      "Consider adding specific metrics for team leadership impact",
      "Highlight architectural decision-making experience"
    ]
  },
  "generated_at": "2024-01-15T11:15:00Z"
}
```

## Data Management Operations

### File Reading and Validation
```typescript
class DataManager {
  async loadPersonalData(): Promise<PersonalData> {
    const contact = await this.readJsonFile('personal/contact.json');
    const skills = await this.readJsonFile('personal/skills.json');
    const experience = await this.readJsonFile('personal/experience.json');
    const education = await this.readJsonFile('personal/education.json');
    
    return this.validateAndMerge({ contact, skills, experience, education });
  }
  
  async savePersonalData(data: PersonalData): Promise<void> {
    await this.writeJsonFile('personal/contact.json', data.contact);
    await this.writeJsonFile('personal/skills.json', data.skills);
    await this.writeJsonFile('personal/experience.json', data.experience);
    await this.writeJsonFile('personal/education.json', data.education);
  }
}
```

### Search and Filtering
```typescript
class ContentMatcher {
  findRelevantSkills(jobKeywords: string[], allSkills: Skill[]): Skill[] {
    return allSkills
      .filter(skill => skill.is_active)
      .map(skill => ({
        ...skill,
        relevanceScore: this.calculateRelevance(skill.keywords, jobKeywords)
      }))
      .filter(skill => skill.relevanceScore > 0.3)
      .sort((a, b) => b.relevanceScore - a.relevanceScore);
  }
  
  findRelevantExperiences(jobRequirements: JobRequirement[], experiences: Experience[]): Experience[] {
    return experiences
      .map(exp => ({
        ...exp,
        relevanceScore: this.calculateExperienceRelevance(exp, jobRequirements)
      }))
      .sort((a, b) => b.relevanceScore - a.relevanceScore);
  }
}
```

## AI Integration with Gemini CLI

### Job Analysis Pipeline
```typescript
class GeminiAnalyzer {
  async analyzeJobDescription(jobText: string): Promise<JobAnalysis> {
    const prompt = `
      Analyze this job description and extract:
      1. Must-have requirements vs preferred qualifications
      2. Technical skills and technologies mentioned
      3. Years of experience required
      4. Leadership/management expectations
      5. Company culture keywords
      
      Job Description:
      ${jobText}
      
      Return structured JSON response.
    `;
    
    const result = await this.callGemini(prompt);
    return this.parseJobAnalysis(result);
  }
  
  async generateSummary(personalData: PersonalData, jobAnalysis: JobAnalysis): Promise<string> {
    const prompt = `
      Generate a compelling 2-3 sentence professional summary for this resume.
      Focus on the most relevant experiences and skills for this specific job.
      
      Personal Background: ${JSON.stringify(personalData, null, 2)}
      Job Requirements: ${JSON.stringify(jobAnalysis.extracted_requirements, null, 2)}
      
      Make it quantifiable and impactful.
    `;
    
    return await this.callGemini(prompt);
  }
}
```

## CLI Interface - Interactive Mode

### Main Commands
```bash
resume-builder init                    # Initialize project structure
resume-builder profile                # Manage personal information
resume-builder skills                 # Manage skills and examples
resume-builder experience            # Manage work experience
resume-builder education             # Manage education and certifications
resume-builder apply                 # Start new job application
resume-builder generate [app-id]     # Generate resume
resume-builder validate [app-id]     # Validate application
resume-builder list                  # List all applications
resume-builder export [app-id]       # Export to different formats
```

### Interactive Application Workflow
```bash
resume-builder apply
```
Interactive prompts:
1. **Basic Info**: Company name, position title, application deadline
2. **Job Description**: Paste text or provide file path
3. **AI Analysis**: Shows extracted requirements with confidence scores
4. **Content Preview**: Shows which skills/experiences will be selected
5. **Customization**: Allow manual overrides and additions
6. **Validation**: Check completeness and relevance
7. **Generation**: Create PDF with progress indicators

## Validation Engine

### Data Validation
```typescript
class ValidationEngine {
  validatePersonalData(): ValidationResult {
    const errors: string[] = [];
    const warnings: string[] = [];
    
    // Required fields check
    if (!this.contact.name || !this.contact.email) {
      errors.push("Name and email are required");
    }
    
    // Skills validation
    const skillsWithoutExamples = this.skills.technical
      .filter(skill => skill.is_active && skill.examples.length === 0);
    if (skillsWithoutExamples.length > 0) {
      warnings.push(`${skillsWithoutExamples.length} skills missing examples`);
    }
    
    // Experience validation
    const unquantifiedAchievements = this.getAllAchievements()
      .filter(achievement => !achievement.impact_metric);
    if (unquantifiedAchievements.length > 0) {
      warnings.push(`${unquantifiedAchievements.length} achievements missing metrics`);
    }
    
    return { errors, warnings, score: this.calculateQualityScore() };
  }
  
  validateJobMatch(applicationId: string): JobMatchResult {
    const jobAnalysis = this.loadJobAnalysis(applicationId);
    const resumeConfig = this.loadResumeConfig(applicationId);
    
    const coverage = this.calculateRequirementsCoverage(
      jobAnalysis.extracted_requirements,
      resumeConfig.selected_skills,
      resumeConfig.selected_experiences
    );
    
    return {
      coverage_percentage: coverage,
      missing_requirements: this.findMissingRequirements(jobAnalysis),
      suggestions: this.generateImprovementSuggestions(jobAnalysis, resumeConfig)
    };
  }
}
```

## LaTeX Template System

### Template Data Interface
```typescript
interface TemplateData {
  personal: ContactInfo;
  summary: string;
  skills: {
    technical: SkillGroup[];
    soft: SkillGroup[];
  };
  experience: FormattedExperience[];
  education: FormattedEducation[];
  customSections?: CustomSection[];
}

interface FormattedExperience {
  company: string;
  title: string;
  duration: string;
  location: string;
  achievements: string[];  // Pre-formatted bullet points
  technologies?: string[];
}
```

### Template Engine
```typescript
class TemplateEngine {
  async generatePDF(templateData: TemplateData, outputPath: string): Promise<void> {
    const latexContent = this.renderTemplate('professional.tex', templateData);
    await this.writeFile(`${outputPath}/resume.tex`, latexContent);
    
    // Generate PDF
    await this.execCommand(`pdflatex -output-directory=${outputPath} ${outputPath}/resume.tex`);
    
    // Cleanup auxiliary files
    await this.cleanupLatexFiles(outputPath);
  }
  
  private renderTemplate(templateName: string, data: TemplateData): string {
    const template = this.loadTemplate(templateName);
    return this.mustacheRender(template, data);
  }
}
```

## Installation & Setup

### Prerequisites
```bash
# System requirements
node --version  # v18+
npm --version   # v8+
pdflatex --version  # LaTeX distribution required

# Gemini CLI setup
npm install -g @google/generative-ai-cli
gemini auth login
```

### Installation
```bash
npm install -g resume-builder-cli

# Initialize new project
mkdir my-resumes && cd my-resumes
resume-builder init

# Follow interactive setup
resume-builder profile setup
```

### Project Initialization
```typescript
class ProjectInitializer {
  async init(): Promise<void> {
    // Create directory structure
    await this.createDirectories([
      'personal',
      'applications', 
      'templates'
    ]);
    
    // Create template files with examples
    await this.createTemplateFiles();
    
    // Interactive data entry
    await this.collectPersonalInformation();
    
    console.log('✅ Project initialized successfully!');
    console.log('Next steps:');
    console.log('  1. Edit personal/*.json files with your information');
    console.log('  2. Run `resume-builder apply` to start your first application');
  }
}
```

## File Backup and Sync

### Version Control Integration
```bash
# Recommended .gitignore
applications/*/resume.pdf
applications/*/resume.tex
applications/*/*.log
node_modules/
.env
```

### Export/Import Functionality
```typescript
class DataPortability {
  async exportProject(outputPath: string): Promise<void> {
    const data = {
      personal: await this.loadPersonalData(),
      applications: await this.loadAllApplications(),
      metadata: {
        exported_at: new Date().toISOString(),
        version: this.getVersion()
      }
    };
    
    await this.writeJsonFile(`${outputPath}/resume-data-export.json`, data);
  }
  
  async importProject(importPath: string): Promise<void> {
    const data = await this.readJsonFile(importPath);
    
    // Validate import data
    await this.validateImportData(data);
    
    // Import with conflict resolution
    await this.importWithBackup(data);
  }
}
```

## Development Phases

### Phase 1: Core Data Management (2-3 weeks)
- JSON schema design and validation
- File I/O operations and error handling
- Basic CLI commands for data entry
- Template personal data files

### Phase 2: AI Integration (2-3 weeks)
- Gemini CLI integration for job analysis
- Content matching algorithms
- Summary generation and content optimization
- Validation engine implementation

### Phase 3: Resume Generation (2 weeks)
- LaTeX template development
- PDF generation pipeline
- File organization and export management
- Interactive generation workflow

### Phase 4: User Experience Polish (1-2 weeks)
- Interactive CLI mode enhancement
- Comprehensive error handling and user guidance
- Documentation and help system
- Cross-platform testing

### Phase 5: Advanced Features (2-3 weeks)
- Data import/export functionality
- Advanced validation and suggestions
- Multiple output formats
- Performance optimization

## Success Metrics

### Technical Quality
- File I/O performance: < 50ms for all data operations
- Resume generation time: < 30 seconds end-to-end
- Cross-platform compatibility: Windows, macOS, Linux
- JSON schema validation: 100% coverage

### User Experience
- Initial setup time: < 10 minutes
- Subsequent applications: < 3 minutes
- Data accuracy: High user satisfaction with AI analysis
- File clarity: Users can easily read and edit JSON files

This JSON-based approach provides transparency, simplicity, and full user control while maintaining the powerful AI-driven features for resume optimization.