# Description

<Please describe the purpose of the PR and what to look out for here.>

# Coding Standards

- [ ] **Readability and Maintainability**: Could **you** maintain this code in the future?
- [ ] **[Hard-coded](https://en.wikipedia.org/wiki/Hard_coding) Values**: Are you relying on them, or on [magic numbers](https://en.wikipedia.org/wiki/Magic_number_(programming))?
- [ ] **System Resources**: 
  - **Disk Space**: Are logs being rotated? Are temporary files cleaned away?
  - **Processor**: Are you closing disused threads? Do you avoid [busy waits](https://en.wikipedia.org/wiki/Busy_waiting)?
- [ ] **[SOLID](https://en.wikipedia.org/wiki/SOLID) Principles**: When creating or modifying an object in code.
- [ ] **Development Junk**: Have work-in-progress logs and comments been cleaned up? *(Looking at you, `print(“milestone b3”)`! )*
- [ ] **Nice File Locations**: Are file locations relative? Do they include any development environment paths, such as "C:/Users/JoeBloggs/projects/..."

## C++

- [ ] **Modern Pointers**: No pointers which are not [smart pointers](https://learn.microsoft.com/en-us/cpp/cpp/smart-pointers-modern-cpp?view=msvc-170#c-standard-library-smart-pointers), unless required for interfacing with another library.
- [ ] **Modern Mutexes**: No locks that are not [scoped locks](https://en.cppreference.com/w/cpp/thread/unique_lock), except where strictly required with explanation.
- [ ] **Parameter Efficiency**:
    - `const` qualifier should be used wherever possible on parameters and member functions.
    - References should be used for all [non-scalar](https://www.oreilly.com/library/view/sql-and-relational/9781449319724/ch02s05.html#:~:text=It%27s%20usual%20to%20think%20of,itself%20is%20scalar%20or%20nonscalar.) types to avoid memory copies.
- [ ] **Documentation**: Is the code commented and documented for future developers? Is it clear, accurate, up-to-date and essential?- [Doxygen](https://www.doxygen.nl/manual/docblocks.html) for C++

## Python
- [ ] **Styling**: [pylint](https://pypi.org/project/pylint/) is strongly recommended during development to enforce the [PEP 8 Style Guide](https://peps.python.org/pep-0008/).
- [ ] **Documentation**: Is the code commented and documented for future developers? Is it clear, accurate, up-to-date and essential?[Docstring](https://peps.python.org/pep-0257/) 

# Testing

- [ ] **Does it run successfully?**
- [ ] **Unit Tests**: 
    - Are there unit tests to cover the new functionality? 
    - Are there unit tests to cover the units that this code interacts with?
- [ ] **System Tests**: 
    - Do they need to be updated to cover this new functionality? 
    - If not, are the current system tests affected?
- [ ] **Error Handling**: Are potential errors handled and logged appropriately for the project?
- [ ] **Unsolvable Issues**: Comment and acknowledge ones that we must live with, for now.

# DevOps

- [ ] **Guides**: Is there a "How To?" for completed scripts, programs, containers.
  - [Swagger](https://swagger.io/) or [OpenAPI](https://spec.openapis.org/oas/v3.1.0)-spec for API changes.
  - [README.md](https://www.markdownguide.org/basic-syntax/) for the relevant repository.

# Security

- [ ] **[Least Privilege](https://csrc.nist.gov/glossary/term/least_privilege#:~:text=Definitions%3A,needs%20to%20perform%20its%20function.)**: When handling authorisation (such as Azure, AWS or database tasks), have you followed this principle?
- [ ] **[Sensitive Data](https://gdpr-info.eu/issues/personal-data/#:~:text=These%20data%20include%20genetic%2C%20biometric,convictions%20or%20trade%20union%20membership.) Handling**:
  - Are we storing any unnecessarily?
  - If so, are these data secured at rest?
  - Are we transmitting any new data unnecessarily across unsafe networks?
  - If so, have we only used [secure connections](https://informationsecurity.wustl.edu/items/confidentiality-integrity-and-availability-the-cia-triad/)?
  - Are all sensitive data kept out of logs?
- [ ] **Data Validation**: When receiving traffic from any external device *(even in a supposed “safe” network)*, are you validating and sanitizing your incoming data?
- [ ] **[Snyk](https://app.snyk.io/login?redirectUri=L29yZy9oYXJyaXNvbmhn&from=snyk_auth_link)**: Does Snyk flag any security concerns in the pull request, or its dependencies?



[Confluence Checklist](https://touchbyte.atlassian.net/wiki/spaces/FaceEntry/pages/34177025/Code+Review+Checklist)
