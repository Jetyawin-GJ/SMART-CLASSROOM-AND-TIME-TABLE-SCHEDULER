# NEP 2020 Compliant Timetable Scheduler

## 🎯 Overview

This enhanced timetable scheduler now fully supports **National Education Policy (NEP) 2020** requirements for elective subjects and flexible curriculum structures. The system provides intelligent scheduling that follows NEP 2020 guidelines for multidisciplinary education.

## 🚀 New Features

### 1. NEP 2020 Elective Types
- **Core Subjects**: Required subjects for the discipline
- **DSE (Discipline-Specific Electives)**: Advanced topics in major field
- **GE (Generic Electives)**: Subjects from other disciplines
- **OE (Open Electives)**: Any subject from any discipline
- **SEC (Skill Enhancement Courses)**: Practical skills and training
- **AEC (Ability Enhancement Courses)**: Language and communication
- **VSC (Vocational Skills Course)**: Industry-specific skills
- **IKS (Indian Knowledge System)**: Traditional knowledge
- **VEC (Value Education Course)**: Ethics and values

### 2. Enhanced Database Models

#### Batch Model (NEP 2020 Fields)
```python
- major_discipline: Primary discipline
- minor_discipline: Secondary discipline  
- total_credits: Total credits for degree (default: 120)
- core_credits: Core subject credits (default: 60)
- elective_credits: Elective credits (default: 40)
- skill_credits: Skill enhancement credits (default: 20)
- is_nep_compliant: NEP 2020 compliance flag
```

#### Subject Model (NEP 2020 Fields)
```python
- elective_type: Type of elective (CORE, DSE, GE, OE, SEC, AEC, etc.)
- course_type: Course type (MAJOR, MINOR, COMMON, ELECTIVE)
- credits: Credit hours for the subject
- discipline: Subject discipline (for GE/OE)
- prerequisites: Prerequisite subjects
- is_interdisciplinary: Cross-disciplinary course flag
- skill_focus: Skill focus for SEC courses
- language_code: Language code for AEC courses
- description: Course description
```

#### Teacher Model (NEP 2020 Fields)
```python
- qualification: Educational qualifications
- specialization: Areas of specialization
- can_teach_electives: Can teach elective courses
- interdisciplinary_expertise: Cross-disciplinary expertise
- language_proficiency: Languages teacher can teach
```

#### New CurriculumOffering Model
```python
- semester: Which semester this is offered
- is_mandatory: Required vs elective
- min_students/max_students: Student limits
- prerequisite_met: Prerequisites satisfied
- credit_hours: Credit hours for this offering
- offering_type: Type of elective
- preferred_time_slots: JSON array of preferred slots
- avoid_time_slots: JSON array of slots to avoid
- room_requirements: Special room requirements
- enrollment_count: Current enrollment
```

### 3. NEP 2020 Scheduler

The new `NEP2020Scheduler` class provides:

- **Intelligent Elective Scheduling**: Prioritizes DSE > GE > OE > SEC > AEC
- **Interdisciplinary Constraints**: Ensures proper spacing between interdisciplinary courses
- **Language Course Optimization**: AEC courses prefer morning slots
- **Skill Lab Scheduling**: SEC labs prefer afternoon slots
- **Credit Tracking**: Monitors credit distribution across elective types
- **Compliance Validation**: Ensures NEP 2020 requirements are met

### 4. New API Endpoints

#### Timetable Generation
- `POST /timetables/generate-nep?batch_id={id}` - Generate NEP 2020 compliant timetable

#### NEP 2020 Data Management
- `GET /data/nep/elective-types` - Get all NEP 2020 elective types
- `GET /data/nep/curriculum-offerings` - Get curriculum offerings
- `POST /data/nep/curriculum-offerings` - Create curriculum offering
- `GET /data/nep/batch-compliance/{batch_id}` - Check NEP compliance

## 🛠️ Setup and Usage

### 1. Database Migration
```bash
# Run NEP 2020 migration
python -m backend.migrate_nep
```

### 2. Test NEP Features
```bash
# Test NEP 2020 scheduler with sample data
python -m backend.test_nep_features
```

### 3. Generate NEP Timetable
```python
from backend.nep_scheduler import generate_nep_timetable
from backend.database import get_db

db = next(get_db())
timetable = generate_nep_timetable(db, batch_id=1)
```

## 📊 NEP 2020 Compliance Features

### Scheduling Constraints
- **Core First**: Core subjects scheduled with highest priority
- **Elective Diversity**: Ensures multiple elective types are offered
- **Interdisciplinary Spacing**: Maintains proper spacing between interdisciplinary courses
- **Language Timing**: AEC courses prefer morning slots
- **Lab Timing**: SEC labs prefer afternoon slots
- **Credit Balance**: Maintains proper credit distribution

### Compliance Validation
The system automatically validates:
- ✅ Core subjects are scheduled
- ✅ Elective diversity (minimum 3 types)
- ✅ Skill enhancement courses present
- ✅ Interdisciplinary spacing maintained
- ✅ Credit requirements met

### Compliance Score
Returns a percentage score based on NEP 2020 requirements:
- 100%: All required elective types present
- 80%: Most elective types present
- 60%: Basic elective structure
- <60%: Needs improvement

## 🎯 Key Benefits

1. **NEP 2020 Compliance**: Fully compliant with National Education Policy 2020
2. **Flexible Curriculum**: Supports major-minor structure with multiple electives
3. **Intelligent Scheduling**: Optimizes scheduling based on NEP guidelines
4. **Credit Management**: Tracks and manages credit distribution
5. **Interdisciplinary Support**: Handles cross-disciplinary course combinations
6. **Skill Enhancement**: Prioritizes practical skill development
7. **Language Learning**: Optimizes language course scheduling
8. **Compliance Monitoring**: Real-time compliance checking

## 🔧 Configuration

### NEP 2020 Constraints
```python
nep_constraints = {
    'max_core_per_day': 2,
    'max_elective_per_day': 2,
    'min_skill_courses_per_week': 1,
    'max_skill_courses_per_week': 3,
    'interdisciplinary_spacing': 1,  # Periods between interdisciplinary courses
    'language_course_timing': 'morning',  # Preferred timing for AEC courses
    'lab_course_timing': 'afternoon'  # Preferred timing for SEC lab components
}
```

## 📈 Example Usage

### Creating NEP 2020 Curriculum
```python
# Create curriculum offering
offering = CurriculumOffering(
    subject_id=subject_id,
    batch_id=batch_id,
    teacher_id=teacher_id,
    semester=3,
    is_mandatory=False,
    credit_hours=3,
    offering_type=ElectiveType.DSE,
    min_students=15,
    max_students=40,
    preferred_time_slots='[{"day": "Mon", "period": 2}]'
)
```

### Checking Compliance
```python
# Check batch compliance
compliance = check_batch_nep_compliance(batch_id, db)
print(f"Compliance Score: {compliance['compliance_score']}%")
```

## 🎉 Success Metrics

- ✅ **100% NEP 2020 Compliance**: All required elective types supported
- ✅ **Intelligent Scheduling**: Optimized scheduling based on NEP guidelines
- ✅ **Flexible Curriculum**: Major-minor structure with multiple electives
- ✅ **Credit Management**: Comprehensive credit tracking and distribution
- ✅ **Interdisciplinary Support**: Cross-disciplinary course combinations
- ✅ **Skill Enhancement**: Practical skill development prioritization
- ✅ **Language Optimization**: AEC course timing optimization
- ✅ **Compliance Monitoring**: Real-time compliance validation

---

**Built with ❤️ for NEP 2020 Implementation**
