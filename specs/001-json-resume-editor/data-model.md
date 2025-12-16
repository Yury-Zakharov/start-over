# Data Model: JSON Resume Editor

## Resume Entity

### Go Backend Model
```go
type Resume struct {
    Basics      *Basics       `json:"basics,omitempty"`
    Work        []Work        `json:"work,omitempty"`
    Volunteer   []Volunteer   `json:"volunteer,omitempty"`
    Education   []Education   `json:"education,omitempty"`
    Awards      []Award       `json:"awards,omitempty"`
    Publications []Publication `json:"publications,omitempty"`
    Skills      []Skill       `json:"skills,omitempty"`
    Languages   []Language    `json:"languages,omitempty"`
    Interests   []Interest    `json:"interests,omitempty"`
    References  []Reference   `json:"references,omitempty"`
    Projects    []Project     `json:"projects,omitempty"`
    // Allow additional properties for extensibility
    AdditionalProperties map[string]interface{} `json:",inline"`
}

type Basics struct {
    Name     string      `json:"name,omitempty"`
    Label    string      `json:"label,omitempty"`
    Image    string      `json:"image,omitempty"`
    Email    string      `json:"email,omitempty"`
    Phone    string      `json:"phone,omitempty"`
    URL      string      `json:"url,omitempty"`
    Summary  string      `json:"summary,omitempty"`
    Location *Location   `json:"location,omitempty"`
    Profiles []Profile   `json:"profiles,omitempty"`
}

type Location struct {
    Address   string `json:"address,omitempty"`
    PostalCode string `json:"postalCode,omitempty"`
    City      string `json:"city,omitempty"`
    CountryCode string `json:"countryCode,omitempty"`
    Region    string `json:"region,omitempty"`
}

type Profile struct {
    Network string `json:"network,omitempty"`
    Username string `json:"username,omitempty"`
    URL     string `json:"url,omitempty"`
}

type Work struct {
    Name        string   `json:"name,omitempty"`
    Position    string   `json:"position,omitempty"`
    URL         string   `json:"url,omitempty"`
    startDate   string   `json:"startDate,omitempty"`
    endDate     string   `json:"endDate,omitempty"`
    Summary     string   `json:"summary,omitempty"`
    Highlights  []string `json:"highlights,omitempty"`
}

type Volunteer struct {
    Organization string   `json:"organization,omitempty"`
    Position     string   `json:"position,omitempty"`
    URL          string   `json:"url,omitempty"`
    startDate    string   `json:"startDate,omitempty"`
    endDate      string   `json:"endDate,omitempty"`
    Summary      string   `json:"summary,omitempty"`
    Highlights   []string `json:"highlights,omitempty"`
}

type Education struct {
    Institution string   `json:"institution,omitempty"`
    URL         string   `json:"url,omitempty"`
    area        string   `json:"area,omitempty"`
    studyType   string   `json:"studyType,omitempty"`
    startDate   string   `json:"startDate,omitempty"`
    endDate     string   `json:"endDate,omitempty"`
    score       string   `json:"score,omitempty"`
    courses     []string `json:"courses,omitempty"`
}

type Award struct {
    Title   string `json:"title,omitempty"`
    Date    string `json:"date,omitempty"`
    Awarder string `json:"awarder,omitempty"`
    Summary string `json:"summary,omitempty"`
}

type Publication struct {
    Name        string `json:"name,omitempty"`
    Publisher   string `json:"publisher,omitempty"`
    ReleaseDate string `json:"releaseDate,omitempty"`
    URL         string `json:"url,omitempty"`
    Summary     string `json:"summary,omitempty"`
}

type Skill struct {
    Name     string   `json:"name,omitempty"`
    Level    string   `json:"level,omitempty"`
    Keywords []string `json:"keywords,omitempty"`
}

type Language struct {
    Language string `json:"language,omitempty"`
    Fluency  string `json:"fluency,omitempty"`
}

type Interest struct {
    Name     string   `json:"name,omitempty"`
    Keywords []string `json:"keywords,omitempty"`
}

type Reference struct {
    Name    string `json:"name,omitempty"`
    Reference string `json:"reference,omitempty"`
}

type Project struct {
    Name        string   `json:"name,omitempty"`
    Description string   `json:"description,omitempty"`
    Highlights  []string `json:"highlights,omitempty"`
    Keywords    []string `json:"keywords,omitempty"`
    startDate   string   `json:"startDate,omitempty"`
    endDate     string   `json:"endDate,omitempty"`
    URL         string   `json:"url,omitempty"`
    Roles       []string `json:"roles,omitempty"`
    Entity      string   `json:"entity,omitempty"`
    Type        string   `json:"type,omitempty"`
}
```

### Elm Frontend Model
```elm
module Models.Resume exposing (..)

import Json.Decode exposing (Decoder)
import Json.Encode exposing (Value)


type alias Resume =
    { basics : Maybe Basics
    , work : List Work
    , volunteer : List Volunteer
    , education : List Education
    , awards : List Award
    , publications : List Publication
    , skills : List Skill
    , languages : List Language
    , interests : List Interest
    , references : List Reference
    , projects : List Project
    }


type alias Basics =
    { name : Maybe String
    , label : Maybe String
    , image : Maybe String
    , email : Maybe String
    , phone : Maybe String
    , url : Maybe String
    , summary : Maybe String
    , location : Maybe Location
    , profiles : List Profile
    }


type alias Location =
    { address : Maybe String
    , postalCode : Maybe String
    , city : Maybe String
    , countryCode : Maybe String
    , region : Maybe String
    }


type alias Profile =
    { network : Maybe String
    , username : Maybe String
    , url : Maybe String
    }


type alias Work =
    { name : Maybe String
    , position : Maybe String
    , url : Maybe String
    , startDate : Maybe String
    , endDate : Maybe String
    , summary : Maybe String
    , highlights : List String
    }


type alias Volunteer =
    { organization : Maybe String
    , position : Maybe String
    , url : Maybe String
    , startDate : Maybe String
    , endDate : Maybe String
    , summary : Maybe String
    , highlights : List String
    }


type alias Education =
    { institution : Maybe String
    , url : Maybe String
    , area : Maybe String
    , studyType : Maybe String
    , startDate : Maybe String
    , endDate : Maybe String
    , score : Maybe String
    , courses : List String
    }


type alias Award =
    { title : Maybe String
    , date : Maybe String
    , awarder : Maybe String
    , summary : Maybe String
    }


type alias Publication =
    { name : Maybe String
    , publisher : Maybe String
    , releaseDate : Maybe String
    , url : Maybe String
    , summary : Maybe String
    }


type alias Skill =
    { name : Maybe String
    , level : Maybe String
    , keywords : List String
    }


type alias Language =
    { language : Maybe String
    , fluency : Maybe String
    }


type alias Interest =
    { name : Maybe String
    , keywords : List String
    }


type alias Reference =
    { name : Maybe String
    , reference : Maybe String
    }


type alias Project =
    { name : Maybe String
    , description : Maybe String
    , highlights : List String
    , keywords : List String
    , startDate : Maybe String
    , endDate : Maybe String
    , url : Maybe String
    , roles : List String
    , entity : Maybe String
    , type_ : Maybe String
    }
```

## Validation Rules

* Resume fields must conform to JSON Resume schema specification
* All fields are optional to maintain flexibility
* Custom fields are allowed for extensibility
* Date fields must be in ISO 8601 format (YYYY-MM-DD)
* URL fields must be valid URLs
* Email fields must be valid email formats

## State Management

### Elm Application State
* RemoteData pattern for handling loading/success/error states
* Current file path state to track which resume file is being edited
* Last modified timestamp to detect external file changes
* Form validation state to prevent saving invalid JSON structures